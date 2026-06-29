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


new branch created 3.7 cloud
Atlas cluster created 
testing 
<img width="763" height="101" alt="image" src="https://github.com/user-attachments/assets/5a721d20-969a-4897-bfaa-71187fe740aa" />

  connected to code and checked 

<img width="1360" height="596" alt="image" src="https://github.com/user-attachments/assets/23bbeb14-a68c-4535-8dd7-40c57ad57a99" />

   deployed in railway.app---image creation on progress

<img width="1363" height="604" alt="image" src="https://github.com/user-attachments/assets/4936f863-eda5-4022-8018-9f1698a60900" />

  properly running in railway.app
  
<img width="1350" height="588" alt="image" src="https://github.com/user-attachments/assets/ec3cb6f3-7523-467b-a49a-168b224c6635" />

----testing-----
stuck with error on pressing shows 
Issue found in manifest.json

   SCRIPT
   "action": {
    "default_popup": "popup.html"
    },
    
  action was not mentioned leading to the issue
  data testing not done

<img width="1354" height="665" alt="image" src="https://github.com/user-attachments/assets/03a95402-490f-48f9-86b4-d6b611265197" />

<img width="1074" height="253" alt="image" src="https://github.com/user-attachments/assets/2e7c2264-38c2-420f-815f-576b94be5081" />

<img width="273" height="583" alt="image" src="https://github.com/user-attachments/assets/8348ea01-bd98-49ce-9c4a-2cad41441f66" />

cluster working 

V3.8 userid json list implementations

V3.9 docker implementations


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

AI-Powered Incident Management System (Future Rollout Plan)


​Overview: This plan outlines the architecture for upgrading the extension to utilize AI auto-scraping, Natural Language Processing (NLP), and Vector Similarity Search. The goal is to scrape HTML content, extract incident context, and dynamically map it to database categories using cosine deviation.


​Phase 1: Auto-Scraping (The Content Script)
​To automate data capture without manual entry, the Chrome Extension API will be utilized to scrape the active page.
​Inject a content.js script into the user's active webpage when the extension is clicked.
​Configure the script to read the DOM and scrape the specific incident ID along with its surrounding description block.
​Pass this raw text payload back to the popup.js frontend via Chrome message passing.


​Phase 2: Meaning Extraction (The LLM Layer)
​Raw HTML scrapes often contain system jargon that needs cleaning.
​Route the raw scraped data from the extension directly to the Express backend.
​Program the backend to make an API call to an external LLM provider.
​Prompt the LLM to analyze the messy text and return a structured summary, such as translating raw logs into "ITM is missing event 15 during create event".


​Phase 3: Vector Embeddings & MongoDB Atlas Integration
​Text summaries must be converted into mathematical arrays (vectors) to compare incident meanings against saved categories.
​Leverage the MongoDB Atlas Free Tier (M0 cluster) environment established in v3.7, which natively supports Atlas Vector Search.
​Command the backend to pass the clean LLM summary to an embedding model, transforming the text into a vector embedding.
​Query this new vector against the existing database of incidents and categories.


​Phase 4: Cosine Deviation & Routing Logic
​Atlas Vector Search compares vectors using Cosine Distance, calculated mathematically as 1 - \text{Cosine Similarity}.
​The backend will determine the relationship between the incident and existing categories using this formula:

Cosine similarity = A.B
                   ----
                   |A||B|


Search ResultSimilarity ScoreBackend ActionExtension UI Display

Close Match> 0.85 (Low Deviation)Map to existing categoryAuto-selects the nearest category in the dropdown.

Partial Match0.70 - 0.85 (Medium Deviation)Fetch nearby categoriesSuggests the top 3 closest existing categories to the user.

High Deviation< 0.70 (No good match)Trigger new category creationPrompts user to add a new AI-generated category name.

Phase 5: Generating and Saving Records
​The user retains ultimate control over the AI's suggestions.
​Ensure the user reviews and clicks "Approve" when a high deviation triggers a new category suggestion.
​Connect the approval action to the existing POST /categories endpoint from the v3.6 build.
​Save the new category to MongoDB, alongside its generated vector embedding.
​Future highly variable incidents of this specific nature will now perfectly map to this new anchor category with minimal deviation.

​Projections & System Constraints
​Latency: Introducing an LLM and vector embedding model will likely add a slight delay (typically 1-3 seconds) between the user clicking the extension and the UI populating with deductions.
​Storage Limits: High-dimensional vector embeddings consume significantly more database storage; database size must be actively monitored to stay within the MongoDB Atlas 512MB free tier limit.
