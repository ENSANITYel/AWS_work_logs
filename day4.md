TASK : Acess shell via termux from my phone providing unlimited access from hands 

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


