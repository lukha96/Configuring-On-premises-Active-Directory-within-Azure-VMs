# Active Directory Deployment and Configuration in Azure

This project demonstrates the deployment and configuration of a **Windows Server Domain Controller** and a **Windows 11 client** in Microsoft Azure.

The lab covers Active Directory Domain Services, DNS configuration, domain joining, organizational units, user administration, Remote Desktop access, and bulk user creation with PowerShell.

## Environments and Technologies Used

- Microsoft Azure
- Windows Server 
- Windows 11
- Active Directory Domain Services (AD DS)
- DNS
- Remote Desktop (RDP)
- PowerShell
- Active Directory Users and Computers (ADUC)

> **Security Note:** Credentials used in this lab were temporary lab credentials and are not included in this repository.

# Configuration Steps

## 1. Create the Azure Network

Create:

- Resource Group
- Virtual Network
- Subnet

Both the Domain Controller and client computer were placed on the same Azure Virtual Network.

<p>
<img width="1537" height="642" alt="image" src="https://github.com/user-attachments/assets/40ceed26-c9e9-4f07-8c79-c340639901d0" />
</p>

## 2. Deploy the Domain Controller VM

Create a Windows Server Virtual Machine named:

`DC-1`

Configure the Network Interface Card (NIC) with a **static private IP address**.

Connect to the server using Remote Desktop.

<p>
<img width="1102" height="692" alt="image" src="https://github.com/user-attachments/assets/41f6ca13-34fa-4680-beb6-a980e9fc7e3a" />
</p>

## 3. Deploy the Client VM

Create a Windows 11 Virtual Machine named:

`Client-1`

Place Client-1 on the same Virtual Network as DC-1.

Configure Client-1's DNS settings to use the private IP address of DC-1.

<p>
<img width="1917" height="660" alt="image" src="https://github.com/user-attachments/assets/24163dc9-42c7-43c2-b9f3-5cf52b6be7c8" />
</p>

## 4. Verify Network Connectivity

From Client-1, ping the private IP address of DC-1.

Example:

`ping <DC-1-Private-IP>`

Verify the DNS configuration with:

`ipconfig /all`

The DNS Server should display DC-1's private IP address.

<p>
<img width="1352" height="696" alt="image" src="https://github.com/user-attachments/assets/0c81dd02-856c-4901-b173-063da8344c15" />
</p>

# Active Directory Installation

## 5. Install Active Directory Domain Services

Login to DC-1 and install:

`Active Directory Domain Services (AD DS)`

Promote DC-1 to a Domain Controller and create a new forest:

`mydomain.com`

Restart the server after the installation.

<p>
<img width="1737" height="912" alt="image" src="https://github.com/user-attachments/assets/70d49b11-b187-4ded-a87c-02b17cfcae39" />
</p>

## 6. Create Organizational Units

Open:

`Active Directory Users and Computers`

Create the following Organizational Units:

- `_EMPLOYEES`
- `_ADMINS`
- `_CLIENTS`

Organizational Units are used to organize users and computers within the domain.

<p>
<img width="845" height="596" alt="image" src="https://github.com/user-attachments/assets/fbb8d0ce-d968-40eb-bb89-56ffde8be646" />
</p>

## 7. Create a Domain Administrator

Create an administrative user account:

`jane_admin`

Place the account inside:

`_ADMINS`

Add the account to the:

`Domain Admins`

security group.

The new Domain Admin account was then used for administrative tasks.

<p>
<img width="871" height="622" alt="image" src="https://github.com/user-attachments/assets/9d519e9a-5e0e-4842-909d-1f1aeffcac41" />
</p>

# Join Client-1 to the Domain

## 8. Join Client-1 to mydomain.com

Login to Client-1 using the local administrator account.

Join the computer to:

`mydomain.com`

Restart Client-1 after joining the domain.

<p>
<img width="1452" height="797" alt="image" src="https://github.com/user-attachments/assets/817b5a1f-6039-490e-85b1-19be76a02c9e" />
</p>

## 9. Verify Client-1 in Active Directory

From DC-1, open Active Directory Users and Computers.

Verify that:

`Client-1`

appears as a domain computer.

Move Client-1 into the:

`_CLIENTS`

Organizational Unit.

<p>
<img width="981" height="705" alt="image" src="https://github.com/user-attachments/assets/455e9548-3c2d-4cd9-9080-38d390fd6b78" />
</p>

# Remote Desktop Configuration

## 10. Configure Remote Desktop for Domain Users

Login to Client-1 using the Domain Administrator account.

Open:

`System Properties → Remote Desktop`

Allow:

`Domain Users`

to access Client-1 through Remote Desktop.

This allows standard domain users to remotely access the workstation.

<p>
<img width="557" height="587" alt="image" src="https://github.com/user-attachments/assets/ac6d6026-50d0-489b-ac1d-e410e49c94d2" />
</p>

# User Administration with PowerShell

## 11. Create Multiple Domain Users

Login to DC-1 using the Domain Administrator account.

Open:

`PowerShell ISE`

as Administrator.

Run a PowerShell script to automatically generate multiple Active Directory user accounts.

The accounts were created inside:

`_EMPLOYEES`

<p>
<img width="1542" height="792" alt="image" src="https://github.com/user-attachments/assets/a2cfdd8e-985f-4653-a0cb-b0b83dc30699" />
</p>

## 12. Verify Users in Active Directory

Open Active Directory Users and Computers and confirm that the new accounts were successfully created inside the `_EMPLOYEES` OU.

<p>
<img width="852" height="597" alt="image" src="https://github.com/user-attachments/assets/0334341f-71bc-4ff5-99c4-a34034868a51" />
</p>

## 13. Test Domain User Login

Select one of the newly created domain accounts and login to Client-1.

Example login format:

`mydomain\username`

Successful login confirms that:

- Client-1 is correctly joined to the domain
- Active Directory authentication is working
- DNS is correctly configured
- Domain users can access the workstation

# Skills Demonstrated

- Azure Virtual Machine deployment
- Virtual Network configuration
- Static IP configuration
- DNS configuration
- Active Directory Domain Services
- Domain Controller deployment
- Active Directory user administration
- Organizational Units
- Security Groups
- Domain joining
- Remote Desktop configuration
- PowerShell automation
- Windows Server administration
- Basic identity and access management

# Project Outcome

Successfully deployed a **Windows Active Directory domain environment in Microsoft Azure** with a Domain Controller and Windows client.

The environment supports centralized authentication, user management, computer management, Remote Desktop access, and automated user creation using PowerShell.
