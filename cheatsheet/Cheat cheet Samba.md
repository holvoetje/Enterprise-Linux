# Cheatsheet for Enterprise Linux

## SAMBA commando's

| Commando | Beschrijving |
|--------|--------|
|yum install samba samba-client samba-common| Installation|
|vi /etc/samba/smb.conf| Change configuration|
|mkdir -p /samba/anonymous| make directory for anonymous share|
|firewall-cmd --permanent --zone=public --add-service=samba| set the firewall|
|firewall-cmd --reload| restart firewall|
|groupadd smbgrp| add the group for secure share|
|useradd admin -G smbgrp| add the user|
|smbpasswd -a fixit| set password|
|mkdir -p /samba/secure_folder| create folder for secure share|
|chmod -R 0777 secure_folder/| set permissions|
|chcon -t samba_share_t secure_folder/| set security context|
|vi /etc/samba/smb.conf| edit configuration|
|testparm| check an smb.conf configuration file for internal correctness|
|getsebool -a `|` grep samba | samba sebools |
