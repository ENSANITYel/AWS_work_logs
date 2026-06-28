EXTENSION PROJECT

created a extension for my project team so that everyone in the team can see the updates over the 
codes so we dont need to ask each other for the querires


functionalities added till now:
 running on localhost 3000 and mongodb


V3.2

   1.add incident , category based on user name and time and its respective details and queries
   2.add incident search
   3.add category search 
   4.add incident updated based on user name

<img width="346" height="399" alt="image" src="https://github.com/user-attachments/assets/62031cba-51ac-4c4b-9739-c723c5f56aff" />

COMPLETED---till now

V3.3
5.added more coloumns in data output make it collapsable so dat when huge data output doesnt cluster

<img width="295" height="134" alt="image" src="https://github.com/user-attachments/assets/cea8f2bc-7768-4356-9fd6-eec38a78970a" />


<img width="296" height="147" alt="image" src="https://github.com/user-attachments/assets/5bf47f37-533f-400b-b610-65a1b5dc950a" />

V3.3--- 24th-06-2026
<img width="296" height="598" alt="image" src="https://github.com/user-attachments/assets/dd1f3bfd-434a-4c45-b340-0f80a34ae8be" />

Modular outputs achived --v3.3

# Deployment Notes

## Overview
This folder contains the deployment and release documentation for the Query Saver extension project.

## Files
- DEPLOYMENT.md — deployment plan, current v3.6 status, and migration notes
- release-plan.md — active release plan for v3.6 and staged v3.7 work

## Current Status
- The current active branch is release/v3.6-only.
- The v3.6 category feature set is working locally.
- The local backend category APIs are verified.
- The extension popup supports category search, category creation, and activity viewing.

## Notes
Use this folder as the main documentation hub for release and deployment updates.

3.6 deployed
<img width="284" height="408" alt="image" src="https://github.com/user-attachments/assets/843e313d-848a-46b0-9a04-52e3e60242a5" />


3.7 planning 
[User clicks "+" button] 
         │
         ▼
 1. popup.js (Extension) captures input ──► Sends HTTPS POST to Railway URL
                                                    │
                                                    ▼
 2. Railway Router ──► Wakes up standard Express port ──► backend/server.js processes route
                                                                    │
                                                                    ▼
 3. Mongoose Driver ──► Uses MONGODB_URI credential ──► Pushes payload into MongoDB Atlas
                                                                    │
                                                                    ▼
 4. MongoDB Atlas ──► Persists data into cluster ──► Returns success status code (201)
                                                                    │
                                                                    ▼
 5. Railway Backend ──► Forwards sanitized JSON payload back to user browser
                                                                    │
                                                                    ▼
[popup.js appends new option into UI accordion/dropdown dynamically]



DATA DIAGRAM

[1. CHROME EXTENSION] 
   │ (User clicks "+" to save an incident/category)

   
[2. SECURE NETWORK REQUEST] 
   │ (popup.js sends an HTTPS request over the internet to your cloud URL)

   
[3. RAILWAY SERVER (Runs 24/7)] 
   │ (backend/server.js processes the data using environment variables)

   
[4. MONGODB ATLAS (Cloud Database)] 
   │ (The data is securely written and permanently saved to your cluster)

   
[5. SUCCESS RESPONSE]
   └── (Server confirms the save and the Extension UI instantly updates)

   
V4.0
test run on AWS ec2 + s3 ---attain total independency

V4.5
test run on different costless service

V5.0
create git dependency



SIDE PROJECT(cyber deck)

Create a total independent linux system to practice bash 
used termux and termux x-11
install ubuntu over termux and running on tablet
installed vscode 
------------------
STILL LEFT 

install chrome 
set up aws on the deck

create an AI agent 
should handle voice chats 
should be total automated 

------------------
REASON: embed AI agent to self recognise cases and provide resolution based on DB source 
under the extension project
