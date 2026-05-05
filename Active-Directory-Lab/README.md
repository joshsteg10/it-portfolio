# Active Directory Lab | Proxmox Homelab

A fully scripted Windows Active Directory environment simulating the identity infrastructure of a mid-size corporation across two branch offices. Built entirely from scratch on Proxmox VE, this lab covers enterprise OU design, role-based access control, tiered NTFS permissions, departmental file shares with Access-Based Enumeration, and end-to-end domain authentication across 115+ user accounts — all provisioned end-to-end with a single PowerShell script.

> **Focus areas:** Enterprise OU design, RBAC, NTFS permissions, file share security, domain authentication, AD automation via PowerShell

---

## Environment

| Component | Details |
|---|---|
| Hypervisor | Proxmox VE |
| Domain Controller | Windows Server (AD DS, DNS) |
| Client Workstation | Windows 10 (domain-joined) |
| Domain | lab.local |
| Services | Active Directory Domain Services, DNS, SMB file sharing, NTFS permissions |

---

## Domain Structure

The domain is organized using a branch-based OU hierarchy that mirrors how enterprise environments segment identity management across physical locations. Each branch contains dedicated OUs for Users, Computers, and Groups. Security groups are nested inside departmental sub-OUs under Groups for clean separation.

```
lab.local
├── Branch1
│   ├── Users
│   ├── Computers
│   └── Groups
│       ├── Finance
│       ├── HR
│       ├── IT
│       ├── Sales
│       └── Marketing
└── Branch2
    ├── Users
    ├── Computers
    └── Groups
        ├── Finance
        ├── HR
        ├── IT
        ├── Sales
        └── Marketing
```

![OU Structure](./images/ou-structure.png)
*ADUC showing both branches fully expanded with Users, Computers, and Groups containers and all five department OUs visible*

---

## User Accounts

Over 115 user accounts are provisioned across both branches covering all five departments. Every account includes a fully populated organizational profile: display name, job title, department, company, office location, manager, email address, phone number, and UPN. Users are placed in the `Users` OU of their respective branch.

![User List](./images/user-list.png)
*Branch1 > Users OU showing populated user accounts with display names visible in the right pane*

Clicking into any user shows a fully populated profile including their manager, department, and title.

![User Properties](./images/user-properties.png)
*User Properties dialog showing the Organization tab with Title, Department, Company, and Manager fields populated*

---

## Security Groups and RBAC

All permission assignments are handled exclusively through security groups. No permissions are ever applied to individual user accounts. Groups follow a strict `BRANCH-DEPARTMENT-ROLE` naming convention, making group purpose immediately identifiable without opening the object.

### Branch 1 Groups (mirrored in Branch 2 with B2 prefix)

| Department | Group | Role |
|---|---|---|
| Finance | B1-Finance-Analysts | Junior analyst access |
| Finance | B1-Finance-Senior-Analysts | Senior analyst access |
| Finance | B1-Finance-Controllers | Controller access |
| Finance | B1-Finance-Auditors | Audit folder access only |
| Finance | B1-Finance-Managers | Full department control |
| HR | B1-HR-Coordinators | General HR access |
| HR | B1-HR-Specialists | Specialist access |
| HR | B1-HR-Recruiters | Recruitment folder access |
| HR | B1-HR-Payroll | Payroll folder access only |
| HR | B1-HR-Managers | Full department control |
| IT | B1-IT-Helpdesk | Tier 1 support access |
| IT | B1-IT-Senior-Helpdesk | Tier 2 support access |
| IT | B1-IT-Network-Engineers | Network infrastructure access |
| IT | B1-IT-Security-Analysts | Security folder access only |
| IT | B1-IT-Systems-Engineers | Systems access |
| IT | B1-IT-Administrators | Full domain control |
| Sales | B1-Sales-Representatives | Standard sales access |
| Sales | B1-Sales-Senior-Representatives | Senior sales access |
| Sales | B1-Sales-Account-Executives | Account folder access |
| Sales | B1-Sales-Business-Development | BD folder access |
| Sales | B1-Sales-Managers | Full department control |
| Marketing | B1-Marketing-Coordinators | General marketing access |
| Marketing | B1-Marketing-Specialists | Specialist access |
| Marketing | B1-Marketing-Content | Content folder access |
| Marketing | B1-Marketing-Digital | Digital folder access |
| Marketing | B1-Marketing-Managers | Full department control |

![Security Groups](./images/security-groups.png)
*Branch1 > Groups > IT OU showing all IT security groups listed in the right pane*

Group membership was verified across departments to confirm all groups are actively populated.

![Group Membership](./images/group-membership.png)
*B1-IT-Helpdesk Members tab showing assigned user accounts*

---

## File Shares and NTFS Permissions

Departmental file shares were created under `C:\Shares\` with a subfolder structure matching real-world usage patterns. Each department has its own dedicated SMB share scoped per branch to enforce data separation between locations. NTFS permissions are applied at both the department root and subfolder level using security groups only. No individual user accounts appear in any ACL.

Access-Based Enumeration (ABE) is enabled on all shares and share-level permissions are scoped tightly per department — a user in IT will only see the IT share when browsing the server. Finance, HR, Sales, and Marketing shares are invisible to them entirely.

### Share Structure

```
C:\Shares\
├── Branch1\
│   ├── Finance\       (share: B1-Finance)
│   │   ├── Reports
│   │   ├── Budgets
│   │   └── Audits        <- restricted: Finance-Auditors and Managers only
│   ├── HR\            (share: B1-HR)
│   │   ├── Policies
│   │   ├── Recruitment
│   │   └── Payroll       <- restricted: HR-Payroll and Managers only
│   ├── IT\            (share: B1-IT)
│   │   ├── Documentation
│   │   ├── Scripts
│   │   └── Security      <- restricted: IT-Security-Analysts and Managers only
│   ├── Sales\         (share: B1-Sales)
│   │   ├── Contracts
│   │   ├── Leads
│   │   └── Reports
│   └── Marketing\     (share: B1-Marketing)
│       ├── Campaigns
│       ├── Content
│       └── Analytics
└── Branch2\
    └── (identical structure with B2 groups)
```

### Permission Tiers

| Level | Permission | Example Groups |
|---|---|---|
| Managers | Full Control | B1-Finance-Managers, B1-IT-Administrators |
| Senior staff | Modify | B1-Finance-Senior-Analysts, B1-IT-Senior-Helpdesk |
| Junior staff | Read and Execute | B1-Finance-Analysts, B1-IT-Helpdesk |
| Restricted subfolders | Modify (scoped group only) | B1-HR-Payroll, B1-IT-Security-Analysts, B1-Finance-Auditors |

Inheritance is disabled on restricted subfolders. Access is explicitly defined so that even senior staff from the same department cannot access payroll, audit, or security data without membership in the specific restricted group.

![NTFS Permissions](./images/permissions.png)
*C:\Shares\Branch1\HR\Payroll Security tab showing B1-HR-Payroll and B1-HR-Managers as the only entries with inheritance disabled*

![Restricted Folder](./images/permissions-restricted.png)
*Advanced Security Settings confirming inheritance is disabled and only two groups hold explicit permissions on the Payroll folder*

---

## Domain Authentication

A Windows 10 workstation was joined to the domain and used to validate authentication across multiple user accounts and roles. Shared resource access was tested per role and unauthorized access attempts were confirmed to be correctly denied. Users browsing to `\\DC\` see only the shares their group has been granted access to — no other department shares are visible.

![Domain Joined](./images/domain-login.png)
*Command prompt output of `systeminfo | findstr /i "domain"` confirming the machine is joined to lab.local*

---

## Validation

- [x] Windows 10 client successfully joined to the domain
- [x] 115+ user accounts provisioned with full organizational profile
- [x] All users assigned to correct security groups based on role
- [x] Manager field populated on all non-manager accounts
- [x] Departmental file shares created and accessible via UNC path
- [x] Share-level permissions scoped per department — users see only their own shares
- [x] Access-Based Enumeration confirmed on all 10 SMB shares
- [x] NTFS permission tiers verified per role
- [x] Restricted subfolders confirmed inaccessible to unauthorized groups
- [x] Unauthorized access attempts correctly denied
- [x] DNS resolution confirmed within the domain

---

## Automation

The entire environment was provisioned using a single PowerShell script. The script handles OU creation, group creation, user provisioning with full attribute population, group membership assignment, manager mapping, file share creation, NTFS permission assignment, and SMB share-level permission lockdown from start to finish with no manual steps.

![PowerShell Script](./images/powershell-run.png)
*PowerShell running Setup-CorpAD.ps1 on the Domain Controller showing completion summary with user and share counts*

---

## Skills Demonstrated

- Active Directory administration (users, groups, OUs, attributes)
- Enterprise OU design with branch and departmental hierarchy
- Role-based access control (RBAC) using security groups
- NTFS permissions with tiered access and restricted subfolder isolation
- SMB file share creation and share-level permission management
- Access-Based Enumeration (ABE) to enforce share visibility per role
- Domain authentication and client management
- PowerShell scripting for AD automation and bulk provisioning
- Virtualization and lab deployment using Proxmox VE

---

## What I Would Expand Next

- Group Policy Objects (GPOs) for password policy enforcement, drive mapping, and desktop lockdown
- Fine-grained password policies scoped per department OU
- Tiered admin model (Tier 0/1/2) to simulate Privileged Access Workstation architecture
- Read-only Domain Controller (RODC) on Branch2 to reflect a real remote-site topology
- Audit policy and Windows Event Log review for logon events and object access
- SIEM integration to forward AD events to a log aggregator
- Helpdesk workflow simulation including password resets, account lockouts, and user provisioning
