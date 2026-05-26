# IT Support Portfolio

IT professional with hands-on experience supporting end users, resolving hardware and software issues, and maintaining technology systems in fast-paced, high-stakes environments. Background in on-site technical support across hotel and conference center operations, where reliable, rapid problem resolution was non-negotiable.

To deepen technical expertise and demonstrate initiative, a fully scripted enterprise Active Directory environment was built from the ground up on Proxmox VE, covering identity management, role-based access control, tiered NTFS permissions, and SMB file share security across 115+ user accounts and two simulated branch offices. Every component was automated via PowerShell with no manual steps.

Holds the Google IT Support Professional Certificate. Committed to continuous learning and building the practical skills that translate directly to IT support and systems administration roles.

---

## Certifications

| Certification | Issuer | Status |
|---|---|---|
| Google IT Support Professional Certificate | Google / Coursera | Completed |
| CompTIA A+ | CompTIA | Core 1 Complete |

---

## Technical Skills

| Category | Skills |
|---|---|
| Operating Systems | Windows 10/11, Windows Server |
| Active Directory | Users, groups, OUs, RBAC, group policy |
| Networking | DNS, DHCP, TCP/IP, connectivity troubleshooting |
| File Systems | NTFS permissions, SMB shares, access control |
| Hardware | Workstations, printers, AV systems, signage displays, peripherals |
| Scripting | PowerShell - automation and bulk provisioning |
| Virtualization | Proxmox VE |
| Support | End-user troubleshooting, user provisioning, account management |

---

## Experience

**Event Services Technician**
Pinnacle Live

Served as the on-site technical support resource across hotel and conference center environments, resolving end-user issues across workstations, printers, networking, and AV systems. Functioned as the first and only point of contact for technology problems during live events, with no escalation path available.

- Resolved end-user issues across hotel business center workstations, printers, and peripheral devices, diagnosing hardware and software problems and restoring service with minimal disruption
- Troubleshot network and connectivity problems affecting client-facing technology, digital signage systems, and event infrastructure
- Diagnosed and resolved AV system failures during live conferences and presentations, identifying root cause and implementing fixes under time-critical conditions
- Configured, deployed, and managed technology systems across multiple concurrent events, ensuring all equipment was operational before client go-live
- Attended BEO (Banquet Event Order) meetings with hotel management to scope technical requirements, coordinate logistics, and ensure all technology needs were planned and fulfilled ahead of events
- Led technical crews during event execution, delegating tasks, managing timelines, and maintaining accountability for all systems throughout the event lifecycle

---

## Projects

### Active Directory Lab | Proxmox Homelab

A fully scripted enterprise Active Directory environment built from scratch on Proxmox VE, simulating the identity infrastructure of a mid-size corporation across two branch offices.

- 115+ user accounts with full organizational profiles (title, department, manager, UPN)
- 50 security groups across 5 departments following `BRANCH-DEPARTMENT-ROLE` naming convention
- Tiered NTFS permissions: Full Control for managers, Modify for senior staff, Read and Execute for junior staff
- Restricted subfolders with inheritance disabled, scoped to specific groups only
- 10 SMB shares with Access-Based Enumeration - users see only the shares they have access to
- Entire environment provisioned end-to-end with a single PowerShell script

**[View project documentation](./Active-Directory-Lab/README.md)**

---

## Lab Roadmap

- Group Policy Objects (GPOs) for password policy enforcement, drive mapping, and desktop restrictions
- Helpdesk simulation scenarios: password resets, account lockouts, permission errors
- Troubleshooting documentation modeled on real-world ticket workflows
- Read-only Domain Controller on Branch2 to simulate a remote site topology
- SIEM integration for log review and event monitoring

---

## Contact

- **LinkedIn:** [LinkedIn](https://www.linkedin.com/in/joshsteg10)
- **Email:** joshsteg10@gmail.com
