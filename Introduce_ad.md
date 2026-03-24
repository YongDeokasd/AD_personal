AD is not designed secure by default

any user within the domain can gather information about AD regardless of their privileges.
Domain Computers	Domain Users
Domain Group Information	Organizational Units (OUs)
Default Domain Policy	Functional Domain Levels
Password Policy	Group Policy Objects (GPOs)
Domain Trusts	Access Control Lists (ACLs)


The Conti Ransomware which has been used in more than 400 attacks around the world has been shown to leverage recent critical Active Directory flaws
such as PrintNightmare (CVE-2021-34527) and Zerologon (CVE-2020-1472) to escalate privileges and move laterally in a target network.
https://www.cisa.gov/sites/default/files/publications/AA21-265A-Conti_Ransomware_TLP_WHITE.pdf
https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-34527
https://msrc.microsoft.com/update-guide/vulnerability/CVE-2020-1472

Active Directory Federation Services (ADFS) was introduced in Server 2008 to provide Single Sign-On (SSO) to systems and applications for users on Windows Server operating systems.
ADFS made it simpler and more streamlined for users to sign into applications and systems, not on their same LAN.
https://en.wikipedia.org/wiki/Active_Directory_Federation_Services
ADFS uses claims based access control model 
https://en.wikipedia.org/wiki/Claims-based_identity

gMSAs is a service to make active directory objects strong such as hardening password policy, account setting, Support deployment to server farms and so on.
https://learn.microsoft.com/en-us/entra/architecture/service-accounts-group-managed

attacking Domain trusts
https://blog.harmj0y.net/redteaming/a-guide-to-attacking-domain-trusts/


AD ACL attacks
https://www.slideshare.net/slideshow/ace-up-the-sleeve/78360130

as-rep-roasting
https://blog.harmj0y.net/activedirectory/roasting-as-reps/

AD Security audit tool (open source - still developed)
https://github.com/netwrix/pingcastle

DC shadow
https://www.dcshadow.com/

Breaking forest trust
https://blog.harmj0y.net/redteaming/not-a-security-boundary-breaking-forest-trusts/

New concept kerberoasting?
https://www.slideshare.net/slideshow/derbycon-2019-kerberoasting-revisited/169869675

RBCD Attack
https://shenaniganslabs.io/2019/01/28/Wagging-the-Dog.html

Empite ( idk how to use it and what's different between other redteaming server and this.. but i need to study it)
https://github.com/BC-SECURITY/Empire

ZeroLogon Vuln
https://www.malwarebytes.com/blog/exploits-and-vulnerabilities/2021/01/the-story-of-zerologon

printnightmare
https://en.wikipedia.org/wiki/PrintNightmare

nopac
https://www.sophos.com/en-us/blog/nopac-a-tale-of-two-vulnerabilities-that-could-end-in-ransomware

Shadow credential
https://specterops.io/blog/2021/06/17/shadow-credentials-abusing-key-trust-account-mapping-for-account-takeover/

cheet sheet
```
Cheat Sheet IAD
Basic Commands Needed

xfreerdp /v:<IP> /u:<User> /p:<Password>
ping <IP>
General Commands

Get-Module
Returns a list of loaded PowerShell Modules.

Get-Command -Module ActiveDirectory
Lists commands for the module specified.

Get-Help <cmd-let>
Shows help syntax for the cmd-let specified.

Import-Module ActiveDirectory Imports the Active Directory Module
Active Directory PowerShell Commands
AD User Commands

New-ADUser -Name "first last" -Accountpassword (Read-Host -AsSecureString "Super$ecurePassword!") -Enabled $true -OtherAttributes @{'title'="Analyst";'mail'="f.last@domain.com"}
Add a user to AD and set attributes.

Remove-ADUser -Identity <name>
Removes a user from AD with the identity of 'name'.

Unlock-ADAccount -Identity <name>
Unlocks a user account with the identity of 'name'.

Set-ADAccountPassword -Identity <'name'> -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "NewP@ssw0rdReset!" -Force)
Set the password of an AD user to the password specified.

Set-ADUser -Identity amasters -ChangePasswordAtLogon $true
Force a user to change their password at next logon attempt.
AD Group Commands

New-ADOrganizationalUnit -Name "name" -Path "OU=folder,DC=domain,DC=local"
Create a new AD OU container named "name" in the path specified.

New-ADGroup -Name "name" -SamAccountName analysts -GroupCategory Security -GroupScope Global -DisplayName "Security Analysts" -Path "CN=Users,DC=domain,DC=local" -Description "Members of this group are Security Analysts under the IT OU"
Create a new security group named "name" with the accompanying attributes.

Add-ADGroupMember -Identity 'group name' -Members 'ACepheus,OStarchaser,ACallisto'
Add an AD user to the group specified.
GPO Commands

Copy-GPO -SourceName "GPO to copy" -TargetName "Name"
Copy a GPO for use as a new GPO with a target name of "name".

New-GPLink -Name "Security Analysts Control" -Target "ou=Security Analysts,ou=IT,OU=HQ-NYC,OU=Employees,OU=Corp,dc=INLANEFREIGHT,dc=LOCAL" -LinkEnabled Yes
Links an existing GPO to the specified OU path. The "-LinkEnabled Yes" ensures that once the link has been established, that the GPO and it's policies are actually enabled (as it is possibe for a GPLink to exist, but at the same time be disabled.)

Set-GPLink -Name "Security Analysts Control" -Target "ou=Security Analysts,ou=IT,OU=HQ-NYC,OU=Employees,OU=Corp,dc=INLANEFREIGHT,dc=LOCAL" -LinkEnabled Yes
Link an existing GPO for use to a specific OU or security group.
Computer Commands

Add-Computer -DomainName 'INLANEFREIGHT.LOCAL' -Credential 'INLANEFREIGHT\HTB-student_adm' -Restart
Add a new computer to the domain using the credentials specified.

Add-Computer -ComputerName 'name' -LocalCredential '.\localuser' -DomainName 'INLANEFREIGHT.LOCAL' -Credential 'INLANEFREIGHT\htb-student_adm' -Restart
Remotely add a computer to a domain.

Get-ADComputer -Identity "name" -Properties * | select CN,CanonicalName,IPv4Address
Check for a computer named "name" and view its properties.
```
