# Checklist Samba - Ruben Holvoet

* Use `netstat -a` to check network settings.
* Try pinging (localhost, ...).
* Check permissions on share > cd to shares root > `ls -al`.
* Check if correct packages are installed (samba, samba-client, samba-common, libsemanage-python) > `yum list installed | grep samba`.
* Check if services are running > `systemctl list-units --type service | grep 'smb|smb'` > if not > `systemctl start smb.service or nmb.service`
* check SELinux sebools > `getsebool -a | grep samba (or smb)` with these enabled: `smbd_anon_write`, `samba_enable_home_dirs`, `use_samba_home_dirs`.
* In `/etc/samba/` of `/usr/local/samba/lib` > `testparm -s [smb.conf]` to check for errors.
* `netstat -tulpn | egrep "samba|smbd|nmbd|winbind"` to check on which ports samba is listening on.
* Firewall: Iptables Open Ports (e.g. 137, 138, 139 and 445) > `vi /etc/sysconfig/iptables` > add for example: `-A RH-Firewall-1-INPUT -s 192.168.1.0/24 -m state --state NEW -p tcp --dport 137 -j ACCEPT` > save file > restart firewall: `service iptables restart` (check firewall rules with `iptables -L -v`)
* Firewall: Show current firewall rules > `firewall-cmd --list-all`.
* Firewall: Enable a port > `firewall-cmd [--permanent] [--zone=ZONE] --add-port=22/tcp`.
* Firewall: Delete a port > `firewall-cmd --remove-port=22/tcp`.
* Use `smbclient -L` to get a list of shares.
* Check logs > `smbd -l /var/log/samba` & `nmbd -l /var/log/samba`.
