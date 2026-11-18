# 📘 Lab Setup: Building the corp.local Domain

<!-- Fill in as you write up the full AD install. Screenshots go in ../images/lab-setup/ -->

## 1. Host & Hypervisor
- Host PC: AMD Ryzen desktop
- VMware Workstation Pro
- Lab network: 192.168.50.0/24 (host-only / custom VMnet)

## 2. DC01: Windows Server 2022
1. Create the VM and install Windows Server 2022
2. Set a static IP: `192.168.50.10`
3. Rename to `DC01`
4. Install the **AD DS** role and promote to a domain controller → new forest `corp.local`
5. Confirm **DNS** is working
6. Install **DHCP**, authorise it, and create a scope for the lab network

## 3. CLIENT01: Windows 11
1. Create the VM and install Windows 11
2. Confirm it gets a DHCP lease from DC01 (e.g. `192.168.50.100`)
3. Rename to `CLIENT01` and join `corp.local`

## 4. Users, OUs & Group Policy
- OUs and test users created
- **Sales GPO** created, linked and verified on CLIENT01 (`gpupdate /force`, `gpresult /r`)

## 5. Verification
- Domain login works on CLIENT01
- DNS resolution and DHCP leases confirmed
