# Full Stack Web Developer Nanodegree - Udacity

## Project: Linux Server Configuration
In this project I set up a Linux server with good security settings, a running web server, and deployment of their Item Catalog project from earlier in the ND, an application that provides a list of items within a variety of categories as well as provide a user registration and authentication system with Facebook. Registered users will have the ability to post, edit and delete their own items, Full CRUD support using SQLAlchemy and Flask and JSON endpoints.

## Prerequisites
I used for creation and runing:
* I used for create my Linux Web Server, Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers. Amazon EC2’s simple web service interface allows you to obtain and configure capacity with minimal friction. It provides you with complete control of your computing resources and lets you run on Amazon’s proven computing environment. 
* Postgres, is an open source object-relational database management system (ORDBMS) with an emphasis on extensibility and standards compliance. It can handle workloads ranging from small single-machine applications to large Internet-facing applications (or for data warehousing) with many concurrent users. Where I created a database for save the appplication info.
* Install Python 3.6 as an interpreted, object-oriented programming language inside the virtual machine.
* Install Flask with pip install Flask as a micro web framework written in Python. It is classified as a microframework because it does not require particular tools or libraries.


# Solution

## Steps
1. Create an Ubuntu Linux server instance on Amazon AWS.
2. Once the instance has started up, follow the instructions provided to conect by SSH  to your server as root user (ubuntu) through ssh: $ ssh -i myproject.pem ubuntu@ec2-3-84-8-127.compute-1.amazonaws.com
4. Create a new user grader with $ sudo adduser grader.
5. Grant udacity the permission to sudo with $ sudo nano /etc/sudoers.d/grader. In the file put in: grader ALL=(ALL:ALL) ALL, then save and quit.
6. Generate public key encripted with 
    - $ ssh-keygen with grader_key
    - P$ cat ~/.ssh/grader_key.pub.
    - Copy and paste the public key and copy it in authorized_keys, and change the permissions:
    - $ sudo chmod 700 /home/grader/.ssh.
    - $ sudo chmod 644 /home/grader/.ssh/authorized_keys.

7. Enforce key-based authentication and disable remote login of root user:

    - $ sudo nano /etc/ssh/sshd_config
    * Change PasswordAuthentication to no.
    * Change PermitRootLogin to no
    - Then, $ sudo service ssh restart.

8. Configure Firewall with
    - $ sudo ufw default deny incoming.
    - $ sudo ufw default allow outgoing.
    - $ sudo ufw allow 2222/tcp.
    - $ sudo ufw allow 80/tcp.
    - $ sudo ufw allow 123/udp.
    - $ sudo ufw enable.

3. Update all packages with:
    - sudo apt-get update
    - sudo apt-get upgrade

4. Configure Apache to serve a Python mod_wsgi application 
    - Install python3.6 $ sudo apt-get install python3.6 
    - Install Apache $ sudo apt-get install apache2
    - Install Mod_WSGI $ sudo apt-get install libapache2-mod-wsgi-py3 and $ sudo a2enmod wsgi
    - Install PIP3 $ sudo apt-get -y install python3-pip
    - Install VirtualEnv $ sudo pip install virtualenv and $ source venv/bin/activate 
    - Start Apache $ sudo service apache2 start

5. I used this commands in web server for flask and Item Catalog Project implementation located on /home/ubuntu/flaskproject
    -  https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps

6. Install and configure PostgreSQL
    - $ sudo apt-get install postgresql postgresql-contrib
    - Acces to PostgreSQL $ sudo -u postgres psql
    - Create a new user called 'grader' with # CREATE USER grader WITH PASSWORD 'grader';
    - Give grader user the CREATEDB permission: # ALTER USER grader CREATEDB; 
    - Create the 'database' database with # CREATE DATABASE database;
    - Change engine = create_engine('sqlite:///database.db') on app.py 'postgresql://grader:grader@localhost/database'
    - Save changes and 
    - Restart Apache $ sudo service apache2 restart
5. Access URL  http://3.84.8.127 from Browser to Item Catalog Project.


## Run

## Notes to Reviewer
- Access Server from SSH with:
    * ssh grader@ec2-3-84-8-127.compute-1.amazonaws.com -p 22  -i ~/.ssh/LinuxCourse
    * Use the public key and password: linux
  - Access Item Catalog Project from Browser with URL http://3.84.8.127.


## References 
* Udacity https://www.udacity.com/
* AWS https://aws.amazon.com/ec2/?nc1=h_ls
* Configuration step 4. https://medium.com/@esteininger/python-3-5-flask-apache2-mod-wsgi3-on-ubuntu-16-04-67894abf9f70
* PostgresSQL https://en.wikipedia.org/wiki/PostgreSQL
