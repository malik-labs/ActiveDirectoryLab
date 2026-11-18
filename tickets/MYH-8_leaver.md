# MYH-8: Disable access for leaver, Mo A

**Type:** Offboarding / Active Directory | **Priority:** High | **Time taken:** 11 minutes | **Status:** Resolved (Done)

**Environment:** VMware home lab, domain `corp.local`. DC01 (Windows Server 2022) and CLIENT01 (Windows 11).

## The report
HR asked for access to be removed for a leaver. Mo A (IT) has a last working day of 18/11/26, and all access must be gone by 17:00. Priority is High because an active account for someone who has left is a security risk.

<p align="center">
<img src="../images/MYH-8/T08g-ticket-as-raised.png" alt="Ticket as raised"/>
<br/><sub>Ticket as raised</sub>
</p>

## Approach
The account is **disabled, not deleted**. Disabling stops sign-in straight away but keeps the account, its history and its permissions record, so it can be audited or re-enabled if the person returns. Then remove its group memberships so nothing still grants access, reset the password, and move the account somewhere obvious so it is easy to find and review.

## What was done

**Find the account.** In Active Directory Users and Computers, Mo A is in the **IT** OU (with Mark C).

<p align="center">
<img src="../images/MYH-8/T08a-leaver-in-it-ou.png" alt="Mo A in the IT OU"/>
<br/><sub>Mo A in the IT OU</sub>
</p>

**Remove group memberships.** In Mo A's properties > **Member Of** tab, the account is in Domain Users and IT-Team. Removed **IT-Team** (confirmation: "Do you want to remove Mo A from the selected group(s)?"). Domain Users stays, because it is the primary group every domain account belongs to.

<p align="center">
<img src="../images/MYH-8/T08b-leaver-group-membership.png" alt="Mo A group membership"/>
<br/><sub>Mo A group membership</sub>
</p>

<p align="center">
<img src="../images/MYH-8/T08c-remove-from-group-confirm.png" alt="Confirm removal from the group"/>
<br/><sub>Confirm removal from the group</sub>
</p>

**Move the account to a Disabled Users OU.** Created a **Disabled Users** OU under CORP and moved Mo A into it, so leavers are kept apart from live users.

<p align="center">
<img src="../images/MYH-8/T08d-disabled-users-ou-created.png" alt="Disabled Users OU created"/>
<br/><sub>Disabled Users OU created</sub>
</p>

**Record it in the description.** Added "Disabled 18/11/26 - leaver" to the account description, so anyone looking at the account later can see when and why it was disabled.

<p align="center">
<img src="../images/MYH-8/T08e-account-in-disabled-users-ou.png" alt="Mo A in Disabled Users with description"/>
<br/><sub>Mo A in Disabled Users with description</sub>
</p>

**Disable the account.** Right-click the user > Disable Account. Active Directory confirms: "Object Mo A has been disabled."

<p align="center">
<img src="../images/MYH-8/T08i-account-disabled-confirmation.png" alt="Account disabled confirmation"/>
<br/><sub>Account disabled confirmation</sub>
</p>

**Reset the password.** Reset Mo A's password to a random value, so the old password cannot be used even if the account is re-enabled by mistake.

<p align="center">
<img src="../images/MYH-8/T08j-reset-password-leaver.png" alt="Reset password"/>
<br/><sub>Reset password</sub>
</p>

## Verification
Tried to sign in on CLIENT01. Windows refuses with "Your account has been disabled. Please see your system administrator."

<p align="center">
<img src="../images/MYH-8/T08f-signin-refused-account-disabled.png" alt="Sign-in refused"/>
<br/><sub>Sign-in refused</sub>
</p>

## Resolution
Closed as Resolved / Done with an internal note.

<p align="center">
<img src="../images/MYH-8/T08h-ticket-resolved.png" alt="Resolved ticket"/>
<br/><sub>Resolved ticket</sub>
</p>

> **Internal note:** 1. Disabled the account in Active Directory Users and Computers. 2. Removed the user from their security groups (kept Domain Users). 3. Moved the account to the Disabled Users OU. 4. Added "Disabled 18/11/26 - leaver" to the account description. 5. Tested sign-in on CLIENT01 - refused, as the account is disabled. Time taken: 11 minutes

## What I learned
- Disable, don't delete. Deleting loses the audit trail and cannot be undone easily.
- Disabling stops sign-in, but group memberships still grant access (for example to shares). Removing them closes that gap.
- A Disabled Users OU and a dated description make leaver accounts easy to find and review later.
- Always test the result. Seeing the "account has been disabled" message is the proof that the job is done.
- Speed matters. HR set a 17:00 deadline, so this is a High priority ticket.

---

<p align="center">
<a href="MYH-7_folder-access-denied.md">← MYH-7: Folder access denied</a> &nbsp;·&nbsp; <a href="../README.md#helpdesk-tickets">All tickets</a>
</p>
