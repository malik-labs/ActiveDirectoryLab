<!-- Add lab diagram here: <p align="center"><img src="images/lab-diagram.png" height="60%" width="60%" alt="Lab network diagram"/></p> -->

<h1>IT Support Home Lab: Active Directory & Helpdesk Ticketing</h1>

This lab copies a small company network so I can practise first-line IT support. I built a Windows Server 2022 domain controller and a Windows 11 workstation in VMware. Then I created realistic faults, logged them as tickets in **Jira Service Management**, and worked through each one: diagnose, fix, document.<br />

<!-- Video section, add when ready:
<h2>Video Demonstration</h2>

- ### [YouTube: IT Support Home Lab Walkthrough](https://youtu.be/YOUR_VIDEO_ID)
-->

<h2>Environments and Technologies Used</h2>

- VMware Workstation Pro (virtualisation)
- Active Directory Domain Services (AD DS)
- DNS & DHCP (Windows Server roles)
- Group Policy Management
- Jira Service Management (ticketing, project key **MYH**)

<h2>Operating Systems Used</h2>

- Windows Server 2022 (DC01)
- Windows 11 (CLIENT01)

<h2>Lab Environment</h2>

| Machine | OS | Role | IP |
|---|---|---|---|
| **DC01** | Windows Server 2022 | Domain Controller (AD DS, DNS, DHCP) for `corp.local` | 192.168.50.10 (static) |
| **CLIENT01** | Windows 11 | Domain-joined workstation | DHCP (192.168.50.100) |

📘 Full build steps: [lab-setup/README.md](lab-setup/README.md)

<h2>Helpdesk Tickets</h2>

| Ticket | Scenario | Category | Write-up |
|---|---|---|---|
| MYH-4 | No network after restart | Networking | 🔜 Screenshots being added |
| MYH-? | Account lockout | Active Directory | 🔜 Coming soon |
| MYH-? | Password reset | Active Directory | 🔜 Coming soon |
| MYH-? | Trust relationship failure | Active Directory | 🔜 Coming soon |
| MYH-? | Group Policy not applying | Group Policy | 🔜 Coming soon |
| MYH-? | Folder sharing / permissions | File Services | 🔜 Coming soon |
| MYH-? | New starter setup | User Lifecycle | 🔜 Coming soon |
| MYH-? | Leaver offboarding | User Lifecycle | 🔜 Coming soon |

<h2>Skills Demonstrated</h2>

- Diagnosing network faults (IP configuration, DHCP, DNS, APIPA addresses)
- Managing users, computers and OUs in Active Directory
- Creating, linking and troubleshooting Group Policy
- Triaging, working and closing tickets in a service desk tool
- Writing clear step-by-step technical documentation
