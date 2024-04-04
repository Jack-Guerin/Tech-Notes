# Windows Server 2022: Active Directory Basics

  * Active Directory (AD)
  * Active Directory Requirements
  * Active Directory Componenets
  * Installing the Active Directory Role
  * Active Directory Management
  * Active Directory Structure and Storage
  * Active Directory Schema
  * Flexible Single Master Operation (FSMO) Roles
  * Global Catalog
  * Directory Object Names
  * Creating User Accounts in Active Directory
  * Creating Groups in Active Directory
  * Assigning Permissions to Users or Groups in Active Directory

## Installing the Active Directory Role [Installing the Active Directory Role]
- Once you install AD on a DC the DC can no longer be renamed.
- Ensure the DC is using a static IP address. AD rRequires DNS to function. THe DNS role can be installed on the DC after the AD role is installed.
    - You can temporarily set the DNS IP address to be the server loopback address until the DNS role is installed and configured.
    - You should always have two domain controllers installed per site.
      - Each DC should have it's preferred DNS server IP set to each other.
      - Set alternate DNS server IP is loopback address.
- 
- 
