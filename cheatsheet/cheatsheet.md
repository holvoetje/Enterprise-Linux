# Cheatsheet for Enterprise Linux

## Git commando's

* cd /c/Users/Ruben/Documents/Github/
* git clone https://github.com/holvoetje/Enterprise-Linux.git
* git remote set-url origin git@github.com:holvoetje/Enterprise-Linux.git

## Vagrant commando's

| Commando | Beschrijving |
| :--- | :--- |
| vagrant up |This command is used to create and configure your guest environment/machines based on your Vagrantfile. |
| vagrant status | This command is used to check the status of the Vagrant managed machines. | 
| vagrant reload | This command is used to do a complete reload on the Vagrantfile. Use this command anytime you make a change to the Vagrantfile. This command will do the same thing as running a halt command and then running an up command directly after. |
| vagrant halt | Executing this is self-explanatory, bring down the environment Vagrant is managing. |
| vagrant suspend | This command suspends the environment instead of shutting it down. Enables a quicker startup of the environment when brought back up later. |
| vagrant resume | Command is used after putting environment in a suspended state. |
| vagrant destroy | Beware. This command will bring down the environment if running and then destroys all of the resources that were created along with the initial creation. |
| vagrant package | This command is used to package a running virtualbox environment in a re-usable box. |
| vagrant ssh | SSH into you vagrant running machines. |

---
* rpm -ql wordpress : Wat geïnstalleerd ?

Filezilla
* ip server: 192.168.56.x
* user: root
* pw: vagrant
* poort: 22
