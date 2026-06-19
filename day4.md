<img width="1346" height="624" alt="image" src="https://github.com/user-attachments/assets/f835aaf9-81cd-40c0-ba02-92b59256f462" />TASK : Acess shell via termux from my phone providing unlimited access from hands 

tried accessing via ssh 
problem 1: inbound rules only my laptop ip 
problem 2: private key ssh pair made
Solution : added new inbound rule from anywhere later on while create a elstic public ip and attach t to shell to reduce privacy 
           and for prvate key issue converted ppk file to pem using online convertor and tarnsported to to termux 
           
           
           SCRIPT : ssh -i private_key.pem ubunu@54.81.125.211

task completed access of my shell via android 


TASK : golden images 
install custom software configs and create a custom ami

SCRIPT sudo dnf install nginx 
       sudo systemctl start nginx
       sudo systemctl enable nginx
       echo "<>hello<>" | sudo tee > /usr/share/nginx/html/index.html
       --clean the bash directory
       history -c && rm -f ~/.bash_history
       sudo find /var/log -type f exec truncate --size 0 {} \;


created a ami 
created a new instance 
and the new instance had the exact data 

<img width="574" height="176" alt="image" src="https://github.com/user-attachments/assets/456c4f8a-7884-416e-b97d-9bf5e0e21588" />


created a volume and connected to shell instance
file -s /dev/xvdf  ----check file path
df -h ----show volumes
mkfs -t ext4 /dev/xvdf  ---format volume
mkdir /mnt/my-data    -created directory
apt-get clean       ----clean
mount /dev/xvdf /mnt/my-data ----mounting


<img width="708" height="394" alt="image" src="https://github.com/user-attachments/assets/6cb05ab2-571e-4b4a-9987-f8c14ea3dbf0" />




TASK : create a launch template using custom ami . set up a auto scaling group tied to alb with min size of 1 and max size of 3

1. created a ami template with
   SCRIPT : #!/bin/bash
            sudo dnf install httpd -y
            sudo systemctl start httpd
            sudo systemctl enable httpd
            sudo echo "<>hi<>" > /var/www/html/index.html

2.creating a auto scaling group based on the 
---ami template 
---with alb and and 
---capacity min as 1 and max as 3 
---based on targetting policies 
    a. cpu utilization 
    b.60 %
    c.cooldown 300 s

added a SNS activity to mail my gmail whenever asg will be targetted

2.auto process failed for some reason so i ec2 connected to one of the asg created instance and tested out to see the script didnt work 
3.redid the entire script to test it out
<img width="1356" height="461" alt="image" src="https://github.com/user-attachments/assets/a7f96d3c-79f0-4d46-99b6-252b671b4fc0" />

this is the proper one 
after creating a script.sh and making it executable by 
 chmod +x scritp.sh

ran it its working 

DEBUG : find why the advanced script .sh didnt work 
The launch template had this
------------ISSUE(h1 is not mentioned to prevent letter issue in git )
#!/bin/bash
sudo dnf install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
sudo echo "<>hi<>" > /var/www/html/index.htnl
-------------
ERROR for the above file 
^CKeyboardInterrupt: Terminated.
Failed to start httpd.service: Unit httpd.service not found.
Failed to enable unit: Unit file httpd.service does not exist.
./myscript.sh: line 5: /var/www/html/index.htnl: No such file or directory

wrote "htnl" inspite of "html"

4.Auto scaling is working
<img width="1346" height="624" alt="image" src="https://github.com/user-attachments/assets/33aebc72-a02e-4701-ad9f-1f1a208e10c5" />


TASK :stress testing ASG and elasticity.
<img width="1136" height="280" alt="image" src="https://github.com/user-attachments/assets/9237a676-c16a-40d2-b0fb-af822cdacc91" />

on stress the new instance is starting 
recieved mail for ASG scaling 
<img width="889" height="404" alt="image" src="https://github.com/user-attachments/assets/2b46244a-d55d-48ef-b40b-68971e7e3f68" />

SNS also tried out

NOTE : fixing ami why script doesnt work
it worked now changed 1 line
#!/bin/bash 
sudo dnf update -y
sudo dnt install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
sudo echo "<>hi<>" > /var/www/html/index.html

<img width="1360" height="718" alt="image" src="https://github.com/user-attachments/assets/bbcfb1e4-21fd-45c7-9e27-852a42e484e7" />


TASK : Learn DNS routing conceptually 
1.
