## Windows Version and Configuration
- Windows version
Systeminfo | findstr /B /C:"OS Name" /C:"OS Version"

- Extract patchs and updates
wmic qfe

- Architecture
wmic os get osarchitecture || echo %PROCESSOR_ARCHITECTURE%

- List all env variables
set
Get-ChildItem Env: | ft Key,value

- List all drives
wmic logicaldisk get caption || fsutil fsinfo drives
wmic logicaldisk get caption,description,providername
Get-PSDrive | where {$_.Provider -like "Microsoft.PowerShell.Core\FileSystem"}| ft Name,Root

## User Enumeration
- Get current username
echo $USERNAME% || whoami
??? why just didn't user whoami?

- List user privilege
  whoami /priv
  whoami /groups

- List all users
net user
whoami /all
Get-LocalUser | ft Name,Enabled,LastLogon
Get-ChildItem C:\Users -Force | select Name : in case the user deleted?

- logon policy
net accounts

- List all local groups
net localgroup
Get-LocalGroup | ft name

- Get details about a group
net localgroup administrators
Get-LocalGroupMember Administrators | ft Name, PrincipalSource

- Get Domain Controllers
nltest /DCLIST:DomainName
nltest /DCNAME:DomainName
nltest /DSGETDC:DomainName





  
