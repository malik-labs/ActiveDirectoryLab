# MYH-5: Restrict Command Prompt access for HR staff

**Type:** Policy request / Group Policy | **Priority:** Low | **Time taken:** 15 minutes | **Status:** Resolved (Done)

**Environment:** VMware home lab, domain `corp.local`. DC01 (Windows Server 2022) and CLIENT01 (Windows 11).

## The report
Requested by the Head of IT. HR staff handle sensitive personal data and have no business need for command-line access (security policy). Scope: all HR staff. Priority is Low because it is a policy request with no service impact.

<p align="center">
<img src="../images/MYH-5/T05g-ticket-open.png" alt="Ticket as raised"/>
<br/><sub>Ticket as raised</sub>
</p>

## Diagnosis
Nothing is broken. This is a least-privilege request. The right tool is a Group Policy Object (GPO) linked to the **HR OU**, because policies apply to OUs, not groups. The HR OU already holds the HR users (Barry Allen and Sarah F), and the OU has no GPOs linked yet.

<p align="center">
<img src="../images/MYH-5/T05a-users-in-hr-ou.png" alt="HR OU members"/>
<br/><sub>HR OU members</sub>
</p>

<p align="center">
<img src="../images/MYH-5/T05b-hr-ou-no-gpo.png" alt="HR OU with no linked GPOs"/>
<br/><sub>HR OU with no linked GPOs</sub>
</p>

## Fix
**1. Create the GPO.** In Group Policy Management, with the HR OU selected, create a new GPO named "HR Restrictions".

<p align="center">
<img src="../images/MYH-5/T05c-new-gpo-hr-restrictions.png" alt="New GPO"/>
<br/><sub>New GPO</sub>
</p>

**2. Enable the setting.** Edit the GPO: User Configuration > Policies > Administrative Templates > System > **Prevent access to the command prompt** = **Enabled**.

<p align="center">
<img src="../images/MYH-5/T05d-prevent-command-prompt-enabled.png" alt="Prevent access to the command prompt: Enabled"/>
<br/><sub>Prevent access to the command prompt: Enabled</sub>
</p>

## Verification
On CLIENT01, sign in as an HR user (Barry Allen).

<p align="center">
<img src="../images/MYH-5/T05e-client-hr-login.png" alt="CLIENT01 sign-in as Barry Allen"/>
<br/><sub>CLIENT01 sign-in as Barry Allen</sub>
</p>

Opening Command Prompt now shows "The command prompt has been disabled by your administrator." Earlier, when he was set up (MYH-2), the same account could run `whoami` in Command Prompt, so this is a before-and-after.

<p align="center">
<img src="../images/MYH-5/T05f-command-prompt-blocked.png" alt="Command prompt blocked"/>
<br/><sub>Command prompt blocked</sub>
</p>

**Control test.** A user outside HR is not affected. Aisha A (Sales) opens Command Prompt and runs `whoami` normally (`corp\aisha`), because the GPO is linked only to the HR OU.

<p align="center">
<img src="../images/MYH-5/T05i-control-aisha-command-prompt.png" alt="Aisha (Sales) can still use Command Prompt"/>
<br/><sub>Aisha (Sales) can still use Command Prompt</sub>
</p>

## Resolution
Closed as Resolved / Done with an internal note.

<p align="center">
<img src="../images/MYH-5/T05h-ticket-resolved.png" alt="Resolved ticket"/>
<br/><sub>Resolved ticket</sub>
</p>

> **Internal note:** 1. Created GPO "HR-Restrictions" in Group Policy Management and linked it to the HR OU. 2. Enabled User Configuration > Administrative Templates > System > "Prevent access to the command prompt". 3. Ran gpupdate /force on CLIENT01; signed in as an HR user - Command Prompt blocked with a restriction message. 4. Signed in as a user outside HR - Command Prompt still works, so the policy is scoped correctly. Time taken: 15 minutes

*Correction: the GPO is named "HR Restrictions" (no hyphen), as the screenshots above show. The hyphen in the note is a typo.*

## What I learned
- Policies attach to OUs. Groups grant access, OUs take policy. That is why the HR users had to be in the HR OU.
- Always test both sides: an affected user is blocked, and an unaffected user is not.
- Least privilege: remove tools users don't need, and record who asked for the change and why.

---

<p align="center">
<a href="MYH-4_no-network-after-restart.md">← MYH-4: No network after restart</a> &nbsp;·&nbsp; <a href="../README.md#helpdesk-tickets">All tickets</a> &nbsp;·&nbsp; <a href="MYH-6_account-lockout.md">MYH-6: Account lockout →</a>
</p>
