# IT Support Portfolio

**Aspiring IT Support Technician** with hands-on experience supporting live event technology across hotel and conference environments, and a homelab built to enterprise standards from the ground up.

I troubleshot real problems under pressure - AV systems going down mid-conference, printers dying in a hotel business center, network issues with no safety net and a room full of people waiting. Now I'm channeling that same instinct into system administration and IT support through self-directed lab work and formal certification.

---

## Certifications

| Certification | Issuer | Status |
|---|---|---|
| Google IT Support Professional Certificate | Google / Coursera | Completed |
| CompTIA A+ | CompTIA | In progress |

---

## Technical Skills

| Category | Skills |
|---|---|
| Operating Systems | Windows 10/11, Windows Server |
| Active Directory | Users, groups, OUs, RBAC, group policy |
| Networking | DNS, DHCP, TCP/IP, troubleshooting connectivity |
| File Systems | NTFS permissions, SMB shares, access control |
| Hardware | AV systems, printers, signage displays, end-user devices |
| Scripting | PowerShell (automation, bulk provisioning) |
| Virtualization | Proxmox VE |
| Ticketing | Helpdesk workflows, user provisioning, account management |

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

**[View project documentation](./active-directory-lab/README.md)**

---

## Experience

**Event Services Technician**
Pinnacle Live

Delivered on-site technical support across hotel and conference center environments, serving as the primary technology resource for clients, venue management, and operational staff. Supported high-profile corporate events where system reliability and rapid issue resolution were critical.

- Provided end-user support for hotel business center operations, including workstation troubleshooting, printer diagnostics and repair, and network connectivity issues
- Troubleshot network and connectivity problems affecting event infrastructure, digital signage systems, and client-facing technology
- Diagnosed and resolved AV system failures in live conference environments with minimal downtime, often under significant time pressure with clients and audiences present
- Managed full lifecycle of AV and signage systems across multiple concurrent events including configuration, deployment, and post-event teardown
- Attended and contributed to BEO (Banquet Event Order) meetings with hotel management to plan and coordinate technical requirements ahead of events, ensuring all AV, networking, and signage needs were scoped and fulfilled
- Led technical crews during event execution, delegating responsibilities, managing setup timelines, and ensuring all systems were operational before client go-live

---

## What I'm Building Toward

The homelab is actively expanding. Next additions:

- Group Policy Objects (GPOs) for password policy, drive mapping, and desktop restrictions
- Helpdesk simulation scenarios: password resets, account lockouts, permission errors
- Troubleshooting documentation modeled on real-world ticket workflows
- Read-only Domain Controller on Branch2 to simulate a remote site topology
- SIEM integration to practice log review and event monitoring

---

## Contact

Open to help desk and IT support roles. Feel free to reach out.

- **GitHub:** github.com/yourusername
- **LinkedIn:** linkedin.com/in/yourprofile
- **Email:** youremail@email.com
