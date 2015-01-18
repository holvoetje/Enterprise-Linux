#Cheat Sheets

## General
Commando's | Uitleg
--------------|----------------
`rpm -ql "naam" `| zoek bestanden in packages
`yum provides *bin/dig`| vindt een package op commando
`ctrl+h`| show hidden files in gnome
`ctrl+l`| provide network path

- LVM rootpartitie aanpassen : http://ubuntuforums.org/showthread.php?t=1537569

## Vagrant
* Sftp naar vagrant machine: `sftp://root@127.0.0.1:2222`

Commando's | Uitleg
--------------|----------------
```vagrant box add --name naamhier locatieboxfile```| Voeg een vagrant box toe
```vagrant init naamhier```| maak je vagrantfile aan
```vagrant up```| start je vagrant box
```vagrant ssh```| ga in je virtual machine
```ctrl+d```| terug naar gitbash
```vagrant halt``` | stop de virtual machine
```vagrant box list``` | namen base boxes tonen
```vagrant status``` | namen base boxes tonen
`vagrant provision *naammachine*`|forces provision provider (ansible)

##Github
- SSH key toevoegen: https://help.github.com/articles/generating-ssh-keys/

Commando's | Uitleg
--------------|----------------
```git add .``` | voeg bestanden toe voor commit
```git commit -m "uitleg aanpassing"``` | git committen
```git push origin master``` | Push naar bitbucket/github
```git pull origin master``` | Pull van bitbucket/github

##Anible Roles
[Ansible Modules](http://docs.ansible.com/modules_by_category.html)

Folder/file| Naam | Uitleg
--------------|----------------|-------------
file |```host_vars/nameserver```| variabelen bruikbaar in de rest van het ansible project
file |```inventory_dev```| apparaten opgesomd
folder|```./roles```| hier horen alle rollen van je machine : beginnen met een KLEINE letter
folder|```./roles/common```| hier horen je standaard zaken zoals selinux, firewall,...
folder|```./roles/'rol'/tasks```| hier hoort de main.yml (Yet another markup language)
folder|```./roles/'rol'/'map'```| er kunenn nog ander mappen zijn zoals handlers, files enz.
file|```./roles/'rol'/tasks/main.yml```| hier komt de modules in voor die taak (zie link hierboven)

##BATS
* Iedere test start met ```@test```    
** Voorbeeld **
	```
    @Test 'The DNS service should be running' {sudo systemctl status 			named.service}
   	```
    
* `${...}` = wordt string     
**Voorbeeld**
```
host= pu001 => &{host}.linuxlab.net
```
* `$(cmd)` = uitvoer van een commando     
 **Voorbeeld**
 ```
 uitvoer=$(cmd)
 ```
* `[ +-= ${something}]` = test   (logische expressies)
* `[ -n ${result}]` = the result can not be empty (enkel strings)
* `[ -z ${something}]`=  empty

##DNS/BIND
* servicenaam: named
* poort 53 firewall 

Commando's | Uitleg
--------------|----------------
```dig @192.0.2.2 pu001.linuxlab.net``` | vraagt A record op
```dig @192.0.2.2 pu001.linuxlab.net NS``` | vraagt NS record op
```dig @192.0.2.2 pu001.linuxlab.net NS +short``` | vraagt NS record op (ip adres only)
`sudo named-checkconf /etc/named.conf`| check config file for mistakes
`/var/named/'zonename'`| zone folder location: past forward and backwards here


##Networking
Commando's | Uitleg
--------------|----------------
```ip addr``` | vervang ifconfig

##Samba
Commando's | Uitleg
--------------|----------------
```setsebool -P allow_smbd_anon_write 1``` | indien shares ingesteld staan op public_content_rw_t
```sudo chcon -R -t public_content_rw_t /srv/shares/delta``` | setsetype op public_content_rw_t
```sudo systemctl restart smb/nmb``` | herstart de service (of start op)
```sudo firewall-cmd --permanent --add-service samba``` | add service samba firewalld
```sudo gpasswd -d bob charlie``` | verwijder user bob uit groep charlie
```sudo chmod 770 alpha``` | verander groep alpha permissions
```smbclient //sutwinsname/sharename --user=bob``` | log in op smb als bob (mkdir proberen voor write)
```getsebool -a |grep samba``` | sebool checken die samba hebben of smb



###config file
server info:
* workgroup name checken

SHARE:
* write list= @group : group krijgt permissies voor write
* valid users= @group : enkel deze group mag aan de share voor read of write
* path= /srv/shares/share: waar je share op de schijf staat
* 


