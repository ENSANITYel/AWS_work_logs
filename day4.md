TASK : Acess shell via termux from my phone providing unlimited access from hands 

tried accessing via ssh 
problem 1: inbound rules only my laptop ip 
problem 2: private key ssh pair made
Solution : added new inbound rule from anywhere later on while create a elstic public ip and attach t to shell to reduce privacy 
           and for prvate key issue converted ppk file to pem using online convertor and tarnsported to to termux 
           
           
           SCRIPT : ssh -i private_key.pem ubunu@54.81.125.211

task completed access of my shell via android 
