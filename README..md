#Linux Server Configuration Project:
in thes project we deploy application into server in amazon .


#Getting Started:
 port:
 2200
###### IP Address:
http://54.93.181.252.xip.io
##### ulr:
http://ec2-54-93-181-252.eu-central-1.compute.amazonaws.com

#summery to steps:
- creat acoount in Amazon Lightsail.
- create Instance
- donwlod the key for acount page
- connect the ```
ssh-i ~/.ssh/your_key.pem aubuntu@4.93.181.252```
-login as root `` sudo su- ``
- ist lkie thise ``root@ip-172-26-0-170:~#``
- adduser grder and give grader superuser
- ``sudo nano /etc/sudoers.d/grader`` add ``grader ALL=(ALL:ALL)ALL`` and save it 
- ``apt-get ubdate
apt-get upgrader
apt-get auto remove``
- in new tirminal run ``ssh-keygen -f ~/.ssh/name_of_key.rsa``
- copy public key then back to ternimal server 
``mkdir .ssh
``
``toush .ssh/authorized_keys`` in  llocat the folder /home/grader
- after that past public key into authorized_keys
- change permissions
``chmod 700 /home/grader/.ssh``
``chmod 644 /home/grader/.ssh/authorized_keys``
``chown -R grader:grader /home/grader/.ssh`` to change owner of ssh folder
- logout root and server 
-now login as grader
``ssh -i ~/.ssh/name_of_key.rsa grader@54.93.181.252``
- ``sudo nano /etc/ssh/sshd-config``
- now we login grader as ``grader@ip-172-26-0-170:$``
- change passwordAuthentication to no 
- change port 22 to 2200
- for permitRoot Login change prohibit-password to no 
``sudo service ssh restart``
- logout then login 
- ``ssh -i ~/.ssh/name_of_key.rsa @54.93.181.252 -p 2200``
- config firewall 
- ``sudo ufw allow 22200/tcp``
- ``sudo ufw allow 80/tcp``
- ``sudo ufw allow 123/tcp``
- ``sudo ufw enable/tcp``
#summery for software we needed:
- ``sudo apt-get insstall apache2``
- ``sudo apt-get insstall libache2-mod-wsgi python-dev``
- ``sudo apt-get insstall git``
- ``sudo apt-get insstall python-pip``
- ``sudo apt-get insstall apache2``
# deploy item catalog project:
- creat new dir catalog in /var/www
- ``sudo chown -R grader:grader catalog`` to change the owner
- ``git clone [project link] catalog``
- then create wasgi fill ``sudo nano catalog.wsgi``

````import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0, "/var/www/catalog/")

from catalog import app as application
application.secret_key = 'supersecretkey'
````

- in database:
 1. ``sudo apt-get install libpq-dev python-dev``
 2. ``sudo apt-get install postgresql postgresql-contrib``
 3. ``udo su - postgres``
 4. ``psql``
 now we login as postgres:
 5. REATE USER catalog WITH PASSWORD 'password';
 6.  ALTER USER catalog CREATEDB;
 7. CREATE DATABASE catalog with OWNER catalog;
 8. \c catalog
 9. REVOKE ALL ON SCHEMA public FROM public;
 10. GRANT ALL ON SCHEMA public TO catalog;
 11. \q
  - then exit
  - after that sudo nano for app.py and database_step.py and manyitems.py
 
 - then change sqlite://catalog.db in create_engine to ``postgresql://catalog:password@localhost/catalog``
 
 - ``sudo service apache2 restart``
 
 ### now connecte to application :
 into broswer http://54.93.181.252.xip.io
 
 #Reference:
best of thank to who posted in github step-by-step
 
 - https://github.com/smilejennyyu/linux-server-configuration
 - https://github.com/mulligan121/Udacity-Linux-Configuration
