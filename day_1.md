1. created a AWS accnt as a root and anther iam user(demo) with root access and created a ec2 instance in ssh connected using putty
2.setup a aws budget for 5 euro and a monthly email alert if ceossed over it
3.create a default vpc and created 2 public subnets in different AZ and connected a route table to it and connected it to a custom igw 
<img width="1148" height="211" alt="image" src="https://github.com/user-attachments/assets/be063ab0-0041-4e95-9a65-b13e263d23ee" />
  create a 2 private subnet under in a different az and connected it to a different route table which is not connected to any az
<img width="1008" height="259" alt="image" src="https://github.com/user-attachments/assets/7c500ec3-1523-4401-a1aa-d7b41c227b93" />

4.create a igw and attach it to vpc . set up a public route table pointng to igw and create subnet under it.

logs from 3 and 4 :subnets need to be under vpc and if they are public needs to ebe connected to a router table to igw basically 
route table is like a wire which connects igw and a subnet telling it has access to outside world
also learnt about ig4 and how 0.0.0.0 works where each zero is a octate and contains 8 digits under it .
so if i say 0.0.0.0 / 16 the vpc has 0.0. initials locked and wont change and the rest two can be changed where subnets can stay .
now if is say subnet 1 has 0.0.0.0/16 i am locking all the ips under vpc 0.0.0.0 in the same subnet and no other subnets can be created .

Advice: create a smaller range subnet if locking /16 as vpc keep the subnets under /24 where third octate can be manipulated and used 
so vpc ---0.0.0.0/16----
and subnet 1 ----0.0.0.0/24----meaning 0.0.0.0 to 0.0.0.255
and availabile subnet possible ranges ----0.0.1.0 to 0.0.255.0

5.create a bastion server where i create a ec2 instance with 
  a.key pair
  b.using a security group having inbound rules as ssh connection allowed from my ip only-----only from my laptop i can access
  c.vpc where the public subnet of 3 work was used which already has a route table and a igw connected to it

  create a private ec2 
  a.same key pair 
  b.using a security group where inbound rules are ssh connected from bastion host ----access private server only via bastion host
  c.attach it to 4 work private subnet

  ssh connect to putty allow forward key attachment

  problem 1 . cant connect via ssh error due to my ip switched
  solution : recretaed a new rule and exclusively attached my ip via (ifconfig) to the inbound rules

  problem 2 . connecting to private server via bastion was not taking the key even though "allow agent forwarding " was turned on.
  solution : pageant application where the bastion key pai was exclusively added and then it worked 

  scripts : ssh -A ec2-user@10.0.4.101

  <img width="786" height="470" alt="image" src="https://github.com/user-attachments/assets/be412667-1471-4e71-84be-3492094fb1c2" />

6.create a 5gb EBS volume check attach it to bastion host log in via ssh ...format the drive and mount it to a directory write a dummy file to it.
scripts: lsblk ---list all disks attached
         sudo file -s /dev/xvdb
         sudo mkfs -t xfs /dev/xvdb
         sudo mkdir /mnt/data5g
         sudo mount /dev/xvdb /mnt/data5g
         df -h ------list all free space 
         sudo chown ec2-user :ec2-user /mnt/data5g-----ownership of the drive 
         echo "Success"> /mnt/data5g/success.txt
         cat /mnt/data5g/succes.5g

 <img width="625" height="379" alt="image" src="https://github.com/user-attachments/assets/31bbeb73-feda-4d9f-bccf-91b785a91000" />

        
         



  
