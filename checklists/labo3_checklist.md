# Labo 3: Troubleshooting checklist
---

- [ ] Are the services running? (Apache, mariaDB, firewall)
      - [ ] `systemctl list-units --type service|grep 'httpd\|mariadb\|firewalld'`

- [ ] Other services not working correctly?
      - [ ] `systemctl list-units --type service`

- [ ] Test the Apache service.
      - [ ] Check IP-address with `ip a` and surf to `https://'IP-Address'`

- [ ] Configure the correct IP-Address (http://ask.xmodulo.com/configure-static-ip-address-centos7.html)
      - [ ] `gedit /etc/sysconfig/network-scripts/ifcfg-enp0s3`
      - [ ] Change these settings:
          - BOOTPROTO="static"
          - IPADRR=192.168.56.14
          - NETMASK=255.255.255.0
          - NM_CONTROLLED=no
          - ONBOOT="yes"
      - [ ] Save file, then restart the service with the command: `systemctl restart network.service`
      - [ ] Re-check the IP-Address with the command: `ip a`

- [ ] Check the Firewall settings
      - [ ] firewall-cmd --permanent --zone=public --add-service=http 
      - [ ] firewall-cmd --permanent --zone=public --add-service=https
      - [ ] firewall-cmd --reload

- [ ] Test PHP
      - [ ] `sudo gedit /var/www/html/test.php`
      - [ ] Create php page by typing this line: `<?php phpinfo(); ?>`
      - [ ] Save and close `test.php`
      - [ ] Surf to `http://IP-Address/test.php`
      - [ ] Remove the info.php file if nescessary with: `sudo rm /var/www/html/test.php`

- [ ] Installing and configuring Apache
      - [ ] `sudo yum install httpd` (install service)
      - [ ] `sudo systemctl start httpd.service` (start service)
      - [ ] `sudo systemctl enable httpd.service` (start service at boot of machine)

- [ ] Installing and configuring PHP
      - [ ] `sudo yum install php php-mysql` (install service)
      - [ ] `sudo systemctl restart httpd.service` (restart service)

- [ ] Installing and configuring mariaDB 
      - [ ] `sudo yum install mariadb mariadb-server` (install service)
      - [ ] `sudo systemctl start mariadb` (start service)
      - [ ] Install mysql through secure installation:
            - `sudo mysql_secure_installation` > `Enter` > `Enter password` > `Re-enter password` > `Enter`
      - [ ] `sudo systemctl enable mariadb` (start service at boot of machine)



