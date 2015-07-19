# Cheatsheet for Enterprise Linux

## Git commando's

* cd /c/Users/Ruben/Documents/Github/
* git clone https://github.com/holvoetje/Enterprise-Linux.git
* git remote set-url origin git@github.com:holvoetje/Enterprise-Linux.git

| Commando | Beschrijving |
| :--- | :--- |
| GIT BASICS |
| git init directory | Create empty Git repo in specified directory. Run with no arguments to initialize the current directory as a git repository. |
| git clone repo | Clone repo located at repo onto local machine. Original repo can be located on the local filesystem or on a remote machine via HTTP or SSH. |
| git config user.name name | Define author name to be used for all commits in current repo. Devs commonly use --global flag to set config options for current user. |
| git add directory | Stage all changes in directory for the next commit. Replace directory with a file to change a specific file. |
| git commit -m "message" | Commit the staged snapshot, but instead of launching a text editor, use <message> as the commit message. |
| git status | List which files are staged, unstaged, and untracked. |
| git log | Display the entire commit history using the default format. For customization see additional options. |
| git diff | Show unstaged changes between your index and working directory. |
| UNDOING CHANGES |
| git revert commit | Create new commit that undoes all of the changes made in commit, then apply it to the current branch.|
| git reset file | Remove file from the staging area, but leave the working directory unchanged. This unstages a file without overwriting any changes. |
| git clean -n | Shows which files would be removed from working directory. Use the -f flag in place of the -n flag to execute the clean. |
| REMOTE REPOSITORIES |
| git remote add name url | Create a new connection to a remote repo. After adding a remote, you can use name as a shortcut for <url> in other commands. |
| git fetch remote branch | Fetches a specific branch, from the repo. Leave off branch to fetch all remote refs. |
| git pull remote | Fetch the specified remote’s copy of current branch and immediately merge it into the local copy. |
| git push remote branch | Push the branch to remote, along with necessary commits and objects. Creates named branch in the remote repo if it doesn’t exist. |

## Vagrant commando's

| Commando | Beschrijving |
| :--- | :--- |
| vagrant box add | allows you to install a box (or VM) to the local machine. |
| vagrant box remove | removes a box from the local machine. |
| vagrant box list | lists the locally installed Vagrant boxes. |
| vagrant init | initializes a project to use Vagrant. |
| vagrant up |This command is used to create and configure your guest environment/machines based on your Vagrantfile. |
| vagrant status | This command is used to check the status of the Vagrant managed machines. | 
| vagrant reload | This command is used to do a complete reload on the Vagrantfile. Use this command anytime you make a change to the Vagrantfile. This command will do the same thing as running a halt command and then running an up command directly after. |
| vagrant halt | Executing this is self-explanatory, bring down the environment Vagrant is managing. |
| vagrant suspend | This command suspends the environment instead of shutting it down. Enables a quicker startup of the environment when brought back up later. |
| vagrant resume | Command is used after putting environment in a suspended state. |
| vagrant destroy | Beware. This command will bring down the environment if running and then destroys all of the resources that were created along with the initial creation. |
| vagrant package | This command is used to package a running virtualbox environment in a re-usable box. |
| vagrant ssh | SSH into you vagrant running machines. |
| vagrant gem | Install Vagrant plugins via RubyGems. |
| vagrant package | Create a distribution of the VM you have running. |
| vagrant <command> –help | Command that will provide man pages for a vagrant command. |
| vagrant rdp | set up RDP with a Windows machine

*To know which package to install*
* yum provides *bin/dig
  * /bin
  * /sbin
  * /usr/bin
  * /usr/sbin

---
* rpm -ql wordpress : Wat geïnstalleerd ?

Filezilla
* ip server: 192.168.56.x
* user: root
* pw: vagrant
* poort: 22

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

## SELinux commando's

| Commando | Beschrijving |
|--------|--------|
| /usr/sbin/sestatus | shows the status of SELinux |
| cat /etc/selinux/config | shows the SELinux config |
| semanage port -l \| grep http | lists the http ports that are managed by SELinux |
| getsebool -a | lists all of the SEbools |
| setsebool [boolean] \[0\|1\] (-P to make it permanent) | sebool instellen | 
| cat /var/log/messages | see the SELinux errors that occured |
| chcon --reference /var/www/html/ /var/www/html/index.html | verander het context type van index.html naar hetzelfde type als de map html |
| restorecon -vR /var/www/html/ | verander context van de map html (+ inhoud) naar de default waarde |
| cat /etc/selinux/targeted/contexts/files/file_contexts (and other files in that directory) | list the default context types |
| ls -Z /var/www/ | list items with their context type |
| semanage fcontext -a -e /var/www/ /foo/ |	add the type of /var/www/ to /foo/, daarna `restorecon -vR /foo/` uitvoeren |
| setenforce 0 | set SELinux to permissive mode (to see errors of all the layers behind a problem) |
| setenforce 1 | set SELinux to enforcing mode |
| vi /etc/selinux/config and set SELINUX=permissive | SELINUX=permissive zetten |
| yum install xorg-x11-xauth policycoreutils-gui bitmap-fixed-fonts, then ssh -X into the box and run system-config-selinux | sets up and starts a gui for SELinux |

## journalctl commando's (logfiles)

1. Check if this folder exists: `/var/log/journal`
2. if not -> `mkdir -p /var/log/journal`
3. Start journal -> `sudo journalctl -f -b -p err -o verbose`
* \-f = telkens updaten
* \-b = enkel logs van current boot
* \-p err = enkel de messages tonen met priority levels ERROR en erger
* \-o verbose = all details the journal has about each entry (user credential info, SELinux bits, ...)
* \-u httpd.service = enkel van de httpd service
