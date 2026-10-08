# Active Directory & IT Support Home Lab

A hands-on IT support project simulating common help desk and Windows system administration tasks in a small business environment.

## Project Overview

I built a virtual IT environment for a fictional company, Murray Technologies, to gain practical experience with Windows Server, Active Directory, networking, user account management, and troubleshooting.

The lab includes a Windows Server 2025 domain controller and a Windows 11 workstation connected through a private VirtualBox network.

I used this environment to simulate employee onboarding, password resets, account lockouts, offboarding, file access permissions, and Group Policy administration.

## Technologies Used

- Windows Server 2025
- Windows 11 Enterprise
- Oracle VirtualBox
- Active Directory Domain Services (AD DS)
- DNS
- Group Policy Management
- Windows PowerShell
- NTFS and SMB file sharing

## Lab Environment

| Device | Operating System | IP Address | Purpose |
|---|---|---|---|
| DC01 | Windows Server 2025 | 192.168.50.10 | Domain Controller, DNS, File Sharing |
| PC01 | Windows 11 Enterprise | 192.168.50.20 | Domain-Joined Workstation |

**Domain:** `murraytech.local`

**Network:** `192.168.50.0/24`

The domain controller uses two network adapters: NAT for internet access and an isolated internal network for communication with PC01.

## Active Directory Configuration

Created a new Active Directory forest and configured organizational units for the fictional company's departments.

Organizational Units:
- Departments
  - IT
  - Sales
  - HR
- Workstations
- Disabled Users

Created fictional employee accounts and assigned users to department-based security groups.

Security Groups:
- SG_IT
- SG_Sales
- SG_HR

Joined a Windows 11 workstation to the domain and verified domain authentication using PowerShell.

## Help Desk Troubleshooting Scenarios

### HD-001: Password Reset
Simulated a forgotten password request, reset the employee's password through Active Directory, required a password change at next sign-in, and verified successful authentication.

### HD-002: Account Lockout
Configured an account lockout policy, simulated repeated failed sign-in attempts, identified the locked account, and restored access using Active Directory and PowerShell.

### HD-003: Employee Onboarding
Created a new employee account, configured account attributes, assigned department security group membership, and verified the employee could sign in to the domain.

### HD-004: Employee Offboarding
Disabled a departing employee's account, removed department security group membership, moved the account to a Disabled Users OU, and verified that new domain sign-in was denied.

## File Sharing and Access Control

Created a Sales department shared folder on Windows Server.

Configured NTFS and SMB share permissions using the SG_Sales security group.

Verified that an authorized Sales employee could access and modify files while an HR employee was denied access.

## Group Policy Configuration

Created a Group Policy Object named `Sales - Map Network Drive`.

Configured Group Policy Preferences to automatically map the Sales shared folder as drive S: for users in the Sales organizational unit.

Verified the mapped drive on PC01 and checked Group Policy application using `gpresult`.

## PowerShell Commands Practiced

```powershell
Get-ADDomain
Get-ADGroupMember -Identity "SG_Sales"
Get-ADUser dwilliams -Properties LockedOut
Unlock-ADAccount -Identity "dwilliams"
Get-ADDefaultDomainPasswordPolicy
Get-SmbShareAccess -Name Sales
gpupdate /force
gpresult /r /scope user
whoami /groups
```

## Project Documentation

- [Screenshots](screenshots/)
- [Help Desk Tickets](tickets/)
- [Network Diagram](diagrams/)

## Skills Demonstrated

- Windows Server administration
- Active Directory user and group management
- Domain-joined workstation configuration
- DNS and basic TCP/IP networking
- Account provisioning and deprovisioning
- Password reset and account lockout troubleshooting
- Group Policy configuration
- NTFS and SMB permissions
- PowerShell administration
- Technical documentation

## Project Summary

This project gave me practical experience building and administering a small Windows domain environment. By completing realistic help desk scenarios, I developed a better understanding of how IT support teams manage employee accounts, troubleshoot authentication problems, and control access to company resources.

All employees, company details, and help desk scenarios in this project are fictional and were created for educational purposes.
