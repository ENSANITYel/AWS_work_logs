task : access mysql db of aws from bastion 
------------------------------------------
1. create  a db security group with private vpc and subnet and inbound rules of bastion instance so only via bastion it can be connected 
2. create  a free tier my sql db in rds with the security group
3. test the connection via bastion host

the security group has been created with the vpc and private subnet 3 and 4 and a free tier my sql db was created under the same security group now testing the db under bastion 

problem : via bastion i am unable to connect since the subnet is public 1 rather than private 3 or 4 
so now i am trying to connect to private instcance that has a connection with private 3 and 4 subnet and trying to connect 

most probably still it will be a issue since the security group was created to have a private connection with bastion rather than private instance .... but lets see

this wont work back to bastion 

errors :
[ec2-user@ip-10-0-1-207 ~]$ mysql -h custom-database-1.cyj8gcoqk7yn.us-east-1.rds.amazonaws.com -P 3306 -u admin -p --ssl-mode=VERIFY_IDENTITY --ssl-ca=./global-bundle.pem
mysql: unknown variable 'ssl-mode=VERIFY_IDENTITY'
[ec2-user@ip-10-0-1-207 ~]$ mysql -h custom-database-1.cyj8gcoqk7yn.us-east-1.rds.amazonaws.com -P 3306 -u admin
ERROR 1045 (28000): Access denied for user 'admin'@'10.0.1.207' (using password: NO)
[ec2-user@ip-10-0-1-207 ~]$ ^[[200~
-bash: $'\E[200~': command not found
[ec2-user@ip-10-0-1-207 ~]$ ~mysql -h custom-database-1.cyj8gcoqk7yn.us-east-1.rds.amazonaws.com -P 3306 -u admin -p --ssl-mode=VERIFY_IDENTITY
-bash: ~mysql: command not found
[ec2-user@ip-10-0-1-207 ~]$ mysql -h custom-database-1.cyj8gcoqk7yn.us-east-1.rds.amazonaws.com -P 3306 -u admin -p --ssl-mode=VERIFY_IDENTITY
mysql: unknown variable 'ssl-mode=VERIFY_IDENTITY'
[ec2-user@ip-10-0-1-207 ~]$ mysql -h custom-database-1.cyj8gcoqk7yn.us-east-1.rds.amazonaws.com -P 3306 -u admin
ERROR 1045 (28000): Access denied for user 'admin'@'10.0.1.207' (using password: NO)
[ec2-user@ip-10-0-1-207 ~]$ mysql -h custom-database-1.cyj8gcoqk7yn.us-east-1.rds.amazonaws.com -p 3306 -u admin
Enter password:
ERROR 1045 (28000): Access denied for user 'admin'@'10.0.1.207' (using password: YES)
[ec2-user@ip-10-0-1-207 ~]$ mysql -h custom-database-1.cyj8gcoqk7yn.us-east-1.rds.amazonaws.com -p 3306 -u admin
Enter password:
ERROR 1049 (42000): Unknown database '3306'


password error fixed 
admin and admin3578

now error with "Unknown database '3306'"


okay got the issue got -p and -P wrong 
 -P--- port 
  -p --password

  to get access 
  Script
  --------------
  mysql -h endpoint -P 3306 -u username -p
  password 

  -------------

  <img width="1106" height="519" alt="image" src="https://github.com/user-attachments/assets/0a20a5a6-7d4b-4bdb-a4ac-6dbd4de79ad0" />


  task completed...

  
task :application load balancers--launch two copy ins and check from web the different insatnce being pulled via load balancer
-----------------------------
1.created a ec2 instance with a vpc and public subnet and a new security grp which has http and ssh connect via my ip
2.dnf update -y 
  dnf install httpd -y
  systemctl start httpd
  systemctl enable httpd
  echo "h1 serer 1 h2" > /var/www/html/index.html

  NOTE :
  🔹 /var
Stores variable data (logs, cache, web content)
  🔹 /var/www
Standard directory where web files are stored
  🔹 /var/www/html
Default web root directory
This is where your website files live
  🔹 index.html
Default homepage file
When someone visits your server IP or domain, this file is shown



2. i created a second server too but i made a mistake is
   i created pre run packet in advance options and did
   #!/bin/bash
   sudo dnf update -y
   dnf install httpd -y
   systemctl start httpd
   systemctl enable httpd
   echo " h1 server 2 h1" > /var/www/html/index.html

    but i didnt use sudo so installing of package failed henceforth the rest of it could have done
-- sudo su
    OR
   used sudo keyword before all the shells


3. for practice i can create an ami and try mistakes --------------------------NEED TO DO AFTER ALB

4.created a target group based on instance 
  with the http 80 and vpc and selected the instance 

5.created a alb with vpc and subnet with both az and connected to the target group

<img width="282" height="89" alt="image" src="https://github.com/user-attachments/assets/3b807461-e759-45e4-bc23-1566a19219b9" />
<img width="239" height="98" alt="image" src="https://github.com/user-attachments/assets/b0feb2cf-1113-4580-a822-4e5f8b42dacb" />

