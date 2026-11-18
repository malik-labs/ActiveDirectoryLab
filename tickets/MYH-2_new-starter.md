# MYH-2: New HR Lead user needs adding to CORP, needs login info ASAP

**Type:** Account creation / Active Directory | **Priority:** High | **Component:** Active Directory | **Time taken:** 9 minutes | **Status:** Resolved (Done)

**Environment:** VMware home lab, domain `corp.local`. DC01 (Windows Server 2022) and CLIENT01 (Windows 11).

## The report
New user: Barry Allen (HR). Reported 3 Nov 2026. He needs to be added to CORP to access his work. Impact: single user unable to work.

<p align="center">
<img src="../images/MYH-2/T02f-ticket-open.png" alt="Ticket as raised"/>
<br/><sub>Ticket as raised</sub>
</p>

## Diagnosis
Nothing is broken. This is a standard new-starter request, so the work is creating the account, making sure it is secure, and putting it in the right place in AD.

## Fix
**1. Create the account.** On DC01, Active Directory Users and Computers > CORP > Users > New > User. First name Barry, last name Allen, logon name `barryallen` (@corp.local).

<p align="center">
<img src="../images/MYH-2/T02a-new-user-wizard.png" alt="New user wizard"/>
<br/><sub>New user wizard</sub>
</p>

<p align="center">
<img src="../images/MYH-2/T02b-new-user-details.png" alt="User details filled in"/>
<br/><sub>User details filled in</sub>
</p>

**2. Set a temporary password and force a change.** The confirmation screen shows "The user must change the password at next logon", then Finish.

<p align="center">
<img src="../images/MYH-2/T02c-new-user-confirm.png" alt="Confirmation screen"/>
<br/><sub>Confirmation screen</sub>
</p>

**3. Place the user in HR.** Moved the user into the HR team (see the internal note below).

<p align="center">
<img src="../images/MYH-5/T05a-users-in-hr-ou.png" alt="Barry Allen in the HR OU (screenshot from MYH-5)"/>
<br/><sub>Barry Allen in the HR OU (screenshot from MYH-5)</sub>
</p>

## Verification
On CLIENT01, Barry signs in with the temporary password and is forced to set a new one ("Your password has been changed").

<p align="center">
<img src="../images/MYH-2/T02d-client-password-changed.png" alt="CLIENT01 password change"/>
<br/><sub>CLIENT01 password change</sub>
</p>

`whoami` returns `corp\barryallen`, so the domain account works.

<p align="center">
<img src="../images/MYH-2/T02e-client-whoami.png" alt="whoami as corp\barryallen"/>
<br/><sub>whoami as corp\barryallen</sub>
</p>

## Resolution
Closed as Resolved / Done with an internal note.

<p align="center">
<img src="../images/MYH-2/T02g-ticket-resolved.png" alt="Resolved ticket"/>
<br/><sub>Resolved ticket</sub>
</p>

> **Internal note:** 1. Created new user account in Active Directory Users and Computers (Barry Allen). 2. Made a temporary unique password. 3. Enabled "must change password at next logon". 4. Moved the user to HR team. 5. Tested login on CLIENT01 - successful. Time taken: 9 minutes.

## What I learned
- New accounts get a temporary password and a forced change, so only the user knows the final password.
- Use a consistent naming format (first name + last name) for logon names.
- Placement matters: the OU decides which policies apply, the group decides what the user can access.

---

<p align="center">
<a href="MYH-1_password-reset.md">← MYH-1: Password reset</a> &nbsp;·&nbsp; <a href="../README.md#helpdesk-tickets">All tickets</a> &nbsp;·&nbsp; <a href="MYH-3_trust-relationship-failure.md">MYH-3: Trust relationship failure →</a>
</p>
