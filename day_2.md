1.create a s3 bucket and host a static website 
 i used the static website in one of my repository i created during my college as hotstar clone
https://github.com/ENSANITYel/HOTSTAR-clone
 i created a bucket and pulled the data from github into local and pasted in bucket and enabled static website hosting
 created a policy using policy generator 
 where action i said get object and bucket i marked as the arn bucket value and generating the below policy

 {
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Allow",
      "Principal": "*",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": "arn:aws:s3:::disnet-stats"
    }
  ]
}


and then while pasting it was showing error as while i was creating the bucket made a mistake a blocked public access.
after turned on i was able to paste the policy and use the link to view the public host

 http://disnet-stats.s3-website-us-east-1.amazonaws.com/


<img width="1346" height="610" alt="image" src="https://github.com/user-attachments/assets/0dfa1148-10e6-4a81-9b0b-fea6054482f0" />


