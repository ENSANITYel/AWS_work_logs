TASK : Learn DNS routing conceptually 

 browser ---> url --- router53 --decides which resource to pull from instead of going to 1 single IP address 
 the disctribtion based on which route53 pulls data from resources can be modified 
      
  1.weighted routing policy ---- we can place percentage based on which the ratio over which the links will be divided can be adjusted
  2.failover routing policy ----active passive failover policy as in whenever health of a single resource goes down it ponts to the next one


 we can mimic route 53 by changing the hosts file and placing a custom hostname straight to aws load balancer

 basically taking the load balancer ip address and assign mock name for the ip

 
 NORMAL
 ---------
 user ---> internet -->route 53--->ALB----> resources
                     (DNS level)

                     
 ROUTE 53 MIMIC
 --------------
 user---> internet ---> system config files (hosts)----> alb ---> resources 
 NOTE : DONT USE A EC2 instance as a system config it will create a bottleneck 

 nslookup alb-test-634172963.us-east-1.elb.amazonaws.com

 <img width="728" height="239" alt="image" src="https://github.com/user-attachments/assets/3991ef9d-da0c-420c-92ea-6d7b0bb9d85b" />

 <img width="802" height="448" alt="image" src="https://github.com/user-attachments/assets/3db78f6a-bb3e-4659-8358-03e015035fb9" />

 modifying this file and adding alb ip address in hosts file would make it work as route 53 

 
TASK : CLEAN UP
--------------


TASK : portfolio website make it static
------------------------------------
uploaded in github 
pushed into aws as a s3 static website 
     
      http://portfolio-website-sabyasachi.s3-website-us-east-1.amazonaws.com/

<img width="1362" height="682" alt="image" src="https://github.com/user-attachments/assets/3b6f4991-c345-4030-951f-91cb9ce04f06" />

