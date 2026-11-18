# MYH-4: CLIENT01 has no network connection after restart

**Type:** Network / DHCP | **Priority:** High | **Time taken:** 14 minutes | **Status:** Resolved

**Environment:** VMware home lab, domain `corp.local`. DC01 (Windows Server 2022, DHCP + DNS) and CLIENT01 (Windows 11).

## The report
Aisha A (Sales) says: *"I started my PC and I can't open anything on the network."* One user affected, unable to reach shares or domain resources.

<p align="center">
<img src="../images/MYH-4/T04g-ticket-open.png" alt="Ticket as raised"/>
<br/><sub>Ticket as raised</sub>
</p>

## Diagnosis

**1. Test basic connectivity.** From CLIENT01, `ping 192.168.50.10` (the DC) failed with "General failure". That error means the PC has no usable network configuration. It is different from "Request timed out", which would mean the network works but nothing replied.

<p align="center">
<img src="../images/MYH-4/T04a-ping-general-failure.png" alt="Ping General failure"/>
<br/><sub>Ping General failure</sub>
</p>

**2. Check the IP configuration.** `ipconfig /all` showed an address of **169.254.162.39** (APIPA), no default gateway and no DHCP server. A 169.254.x.x address means the client asked for an address and nobody answered.

<p align="center">
<img src="../images/MYH-4/T04b-ipconfig-apipa.png" alt="ipconfig showing APIPA"/>
<br/><sub>ipconfig showing APIPA</sub>
</p>

**3. Check the server that should answer.** In VMware, DC01 was **Powered off**. DC01 runs DHCP and DNS for the lab, so this was the likely cause.

<p align="center">
<img src="../images/MYH-4/T04c-dc01-powered-off.png" alt="DC01 powered off"/>
<br/><sub>DC01 powered off</sub>
</p>

## Cause
DC01 (the DHCP and DNS server) was powered off, so CLIENT01 could not get a DHCP lease and fell back to an APIPA address.

## Fix
Started DC01 and waited for it to finish booting. Confirmed on DC01 that it had its static address, 192.168.50.10.

<p align="center">
<img src="../images/MYH-4/T04d-dc01-ip.png" alt="DC01 IP after boot"/>
<br/><sub>DC01 IP after boot</sub>
</p>

CLIENT01 then obtained a lease from DC01 (192.168.50.100).

<p align="center">
<img src="../images/MYH-4/T04e-client-lease.png" alt="CLIENT01 lease"/>
<br/><sub>CLIENT01 lease</sub>
</p>

## Verification
`ping 192.168.50.10` from CLIENT01 returned 4 replies, 0% loss.

<p align="center">
<img src="../images/MYH-4/T04f-ping-success.png" alt="Ping success"/>
<br/><sub>Ping success</sub>
</p>

## Resolution
Documented and closed in Jira Service Management with the internal note below.

<p align="center">
<img src="../images/MYH-4/T04h-ticket-resolved.png" alt="Resolved ticket"/>
<br/><sub>Resolved ticket</sub>
</p>

> **Internal note:** Checked: ping 192.168.50.10 failed with "General failure". ipconfig /all showed 169.254.162.39 (APIPA), no default gateway, and no DHCP server address. Cause: DC01 (the DHCP and DNS server) was powered off, so the client could not get a DHCP lease. Fix: started DC01 and waited for it to boot; confirmed it had 192.168.50.10; CLIENT01 then obtained 192.168.50.100. Verified: ping to DC01 replies. Time taken: 14 minutes

## What I learned
- A 169.254.x.x address on a domain PC means DHCP did not answer. Check the DHCP server before touching the client.
- "General failure" and "Request timed out" mean different things, and telling them apart narrows the fault quickly.
- In the lab, start DC01 first and shut it down last. In a real environment this is the "server is down, so everyone's PC loses the network" case.

---

<p align="center">
<a href="MYH-3_trust-relationship-failure.md">← MYH-3: Trust relationship failure</a> &nbsp;·&nbsp; <a href="../README.md#helpdesk-tickets">All tickets</a> &nbsp;·&nbsp; <a href="MYH-5_restrict-command-prompt-hr.md">MYH-5: Restrict Command Prompt for HR (GPO) →</a>
</p>
