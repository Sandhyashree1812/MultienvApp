# Multi-Environment Application Deployment

A containerized multi-environment application deployed on AWS EC2 using Docker Compose.

## Project Overview

The application contains three services:

1. **Development Backend** â€“ Flask application connected to the development MongoDB database (port 3001).
2. **Production Backend** â€“ Flask application connected to the production MongoDB database (port 3002).
3. **Frontend** â€“ React application served by Nginx on port 3000, routing API requests to the appropriate backend.

## Live Deployment

- Frontend: http://3.89.62.29:3000
- Development: http://3.89.62.29:3000/dev
- Production: http://3.89.62.29:3000/prod

## Architecture

The React frontend communicates with both Flask backends through Nginx reverse proxy routes. Docker Compose runs all three services on a shared bridge network.

## Project Structure

## Project Structure

```text
MultienvApp/
|
+-- backend/
|   +-- dev/
|   |   +-- app.py
|   |   +-- requirements.txt
|   |   +-- Dockerfile
|   |
|   +-- prod/
|       +-- app.py
|       +-- requirements.txt
|       +-- Dockerfile
|
+-- frontend/
|   +-- public/
|   +-- src/
|   +-- package.json
|   +-- nginx.conf
|   +-- Dockerfile
|
+-- Screenshots/
|
+-- submission/
|   +-- submission-info.txt
|
+-- .env.example
+-- .gitignore
+-- docker-compose.yml
+-- README.md
```


Phase 1 AWS EC2 infrastructure setup

Step 1. Launch an EC2 instance

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/080689e6-9dc9-4e76-8580-7f0c5bd9e9fb" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1becc349-ebc7-4f32-b8e8-bf579094d827" />
Security Group and inbound rules:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1fc75b93-f159-49ae-8fc2-948e557a81b8" />

Phase 2 Connect to EC2 using SSH

Run: ssh -i "$env:USERPROFILE\Downloads\multienv-key.pem" ubuntu@3.89.62.29

<img width="778" height="143" alt="image" src="https://github.com/user-attachments/assets/1672215d-2967-4e5d-bff4-62cb642f0aa2" /> 

<img width="873" height="320" alt="image" src="https://github.com/user-attachments/assets/c6fe2a11-2f42-4ec4-8875-e94704f7b651" />

<img width="755" height="241" alt="image" src="https://github.com/user-attachments/assets/747ee5f1-8bb1-4916-ac50-819f11283d3f" />


Phase 3 Verify server resources

1. Verify username
   Run: whoami
<img width="303" height="56" alt="image" src="https://github.com/user-attachments/assets/d7a5ec56-9346-43b2-a489-00e72079eb16" />


3. Verify Ubuntu version
Run: lsb_release -a

<img width="359" height="112" alt="image" src="https://github.com/user-attachments/assets/4b2d54a0-13d5-432b-883e-e7a9f1f263b0" />



3. Verify CPU
   Run: nproc
   <img width="258" height="50" alt="image" src="https://github.com/user-attachments/assets/11fc22c8-9072-4c64-9bec-1b11f3914832" />

4. Verify RAM
   Run: free -h
   <img width="649" height="74" alt="image" src="https://github.com/user-attachments/assets/e584bf70-8298-476c-a1cd-3e77fcd01a85" />

5. Verify disk
   Run: df -h

   <img width="579" height="172" alt="image" src="https://github.com/user-attachments/assets/9d0faedb-c41c-4943-98b4-d97f6ce3d1ae" />

Phase 2 Install Docker and Docker Compose

Step 1. Update Ubuntu
Run: sudo apt update

Step 2. Install prerequisites
Run:
sudo apt install -y ca-certificates curl git

Step 3. Install Docker Engine and Compose
Run:
sudo apt install -y docker.io docker-compose-v2 

Step 1. Start Docker
sudo systemctl enable --now docker
Step 2. Check Docker service status
sudo systemctl status docker 

<img width="883" height="411" alt="image" src="https://github.com/user-attachments/assets/69f1851b-a87b-40bd-81d4-bae76f847133" />

Step 3. Configure Docker permissions
sudo usermod -aG docker $USER
Apply the new group membership:
newgrp docker

Step 4. Verify Docker
docker --version

Step 5. Verify Docker Compose
docker compose version

<img width="404" height="117" alt="image" src="https://github.com/user-attachments/assets/6d060b8d-9cec-472f-b9bb-15c8293e7409" />

Step 1 Clone the repository
git clone https://github.com/Sandhyashree1812/MultienvApp.git

Step 2 Enter the project directory
cd MultienvApp

<img width="622" height="290" alt="image" src="https://github.com/user-attachments/assets/266baf07-4dc7-4fad-b577-03a2d2f6f597" />


Step 3 Inspect the project structure
Run: ls -la

<img width="393" height="229" alt="image" src="https://github.com/user-attachments/assets/fddde056-f1ea-4fea-aabf-b445783b49d6" />



Run: find . -maxdepth 4 -type f | sort

Step 4 Check available memory and disk space
free -h
df -h /  

<img width="398" height="427" alt="image" src="https://github.com/user-attachments/assets/e1ef1a49-05e0-4f05-9bc7-b03d2966fcd1" />


4. Inspect the backend and frontend files
cat backend/dev/app.py
cat backend/dev/requirements.txt
cat backend/prod/app.py
cat backend/prod/requirements.txt
cat frontend/package.json

2. Inspect the React API configuration
Run these commands in your EC2 Ubuntu terminal:
cd ~/MultienvApp

cat frontend/src/App.js
cat frontend/src/pages/Home.js
cat frontend/src/pages/Tickets.js

2. Fix the React API URLs:
   The code used in frontend/src/pages/Tickets.js. is as below, this makes the browser send API requests through Nginx:
   
   const apiUrl =
  env === "dev"
    ? "/api/dev/tickets"
    : "/api/prod/tickets";

--------------------------------------------- 

3. Create the backend Dockerfiles
   frontend/src/pages/Tickets.js.
   Create the backend Dockerfiles
   Create backend/dev/Dockerfile
   Create backend/prod/Dockerfile

4. Create the frontend Dockerfile
Create frontend/Dockerfile
Create frontend/nginx.conf:

. MongoDB Atlas connection strings

 Step 1 Create a new MongoDB Atlas project

 <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4adf0872-4838-4672-94bd-18766d89a3cb" /> 

 
 Step 2 creating your MongoDB cluster

Step 3 Choose Drivers and Client Libraries
Select Python as the driver.
- Language: Python
- Client Library: PyMongo (Synchronous)
Choose the recommended version if asked.

Copy the connection string
1. Find the Copy button beside the connection string.
2. Click it.
3. Paste it temporarily into Notepad on your computer.
4. Replace the username and password placeholders with your actual database user credentials.

Step 1 Copy your connection string

Step 2 â€” Prepare two database URLs

We'll use the same cluster but separate databases.

Your development connection string should end with:
mongodb+srv://USERNAME:PASSWORD@YOUR_CLUSTER.mongodb.net/multienv_dev?retryWrites=true&w=majority
Your production connection string should end with:
mongodb+srv://USERNAME:PASSWORD@YOUR_CLUSTER.mongodb.net/multienv_prod?retryWrites=true&w=majority

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/69f436b7-f163-4604-9682-d7dd9825458f" />


Step 4 â€” Allow your EC2 server
This is important. Your EC2 server must be authorized separately.
1. In Atlas, open Security â†’ Network Access.
2. Click Add IP Address : 3.89.62.29/32

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/31dfbc1b-58d1-4945-8806-4ba19c34fa88" /> 

In the Comment field, enter:
MultienvApp-EC2

Step 2 â€” Temporary access setting
You can leave this switch OFF.

That means the IP access entry won't automatically expire after six hours.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3b26c229-aa68-482c-b836-0cae18131ba2" />


Step 3 â€” Confirm
Click the green Confirm button.

Step 4 â€” Verify database user
After confirming the IP:
1. Click Database Users in the left menu.
2. Check whether you already have a database user.

   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/20c6c340-156e-4030-a1ac-b8bae7b38d73" />

   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/34398dcc-b741-456d-b186-833893d26250" />



Step 1 â€” Create an application database user
Click + ADD NEW DATABASE USER at the top right.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/69572a19-b472-4079-9c50-43db334cc937" />




Step 1 â€” Assign the database role
1. Scroll slightly up in the user creation window.
2. Find Built-in Role.
3. Click Add Built In Role.
4. Open the role dropdown.
5. Select:
Select this role: 
Read and write to any database

Step 2 â€” Keep the other settings unchanged
- Custom Roles: Leave unchanged.
- Specific Privileges: Leave unchanged.
- Restrict Access to Specific Clusters: OFF.
- Temporary User: OFF.

  Step 3 â€” Create the user
Scroll to the bottom and click the green Add User button.

   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/62a85c57-718d-4483-91f1-58b4e1307c38" />


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6d40f0d0-4fac-4013-8213-3a23fbf28104" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b1680a0a-f579-499b-9588-3744736728c8" />


Configure MongoDB on your EC2 server
Step 1 â€” Get the connection string
1. Open Database â†’ Clusters.
2. Find MultienvCluster.
3. Click Connect.
4. Select Drivers.
5. Choose Python and PyMongo.
6. Copy the connection string.

7. <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0c5c7487-ed2c-4234-b9e3-a79a18f3a5cf" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/138b1e4e-f800-457a-aa8c-27cdb7e1af87" /> 

------------------------ 

Note: As the EC2 instance got stopped again the Public IPv4 address changed, so used the new one from here:
Updated MongoDB Atlas also with the chnaged IP address
Checked on Docker
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/37b70f69-34da-439c-a88b-f786dee3ed89" /> 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/eab08ffc-8704-4159-963b-16364e17de59" />

<img width="357" height="42" alt="image" src="https://github.com/user-attachments/assets/1e93dac2-e602-4130-9d2c-4bc8d5cd3308" />

<img width="328" height="36" alt="image" src="https://github.com/user-attachments/assets/08a3323e-cf45-4d3a-a436-1180958fa203" /> 

<img width="311" height="427" alt="image" src="https://github.com/user-attachments/assets/7e036084-77b9-4d3a-886c-75a431a9db25" />



EC2 instance has again restarted and its new public IP address is:
3.89.62.29
Previous IP: 23.22.159.171 · New IP: 3.89.62.29 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/caecb981-598d-4bb1-904d-b40245a3b037" /> 

Updated the EC2 security group:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2a0355f6-6e8a-43cb-a50c-710e0c6c9f05" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/49b0aa5e-786b-442e-9835-3a4d511cbfae" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/91aff556-c347-4f4b-bed9-081804aaa17e" />

----------------------------------- 

   Prepare the two database URLs
We'll use separate databases:
- multienv_dev
- multienv_prod

  Step 3 Create the environment file on EC2
Return to your Ubuntu SSH terminal and run:  nano .env

add the below code, replacing the password:
DEV_MONGO_URI="mongodb+srv://USERNAME:YOUR_PASSWORD@YOUR_CLUSTER.mongodb.net/multienv_dev?retryWrites=true&w=majority"

PROD_MONGO_URI="mongodb+srv://USERNAME:YOUR_PASSWORD@YOUR_CLUSTER.mongodb.net/multienv_prod?retryWrites=true&w=majority"

save: Cntrl+O
file name prompt is shown as .env: press enter
exit: Cntrl +X

<img width="323" height="138" alt="image" src="https://github.com/user-attachments/assets/c6b72698-2ad2-45f3-b2b9-bef5a54dbbe3" />

<img width="325" height="334" alt="image" src="https://github.com/user-attachments/assets/27662313-c6f0-45d7-b1aa-a31c1ce132bd" />


Phase 2 â€” Fix the application configuration


Step 2.1 Update the development backend
Run this in your EC2 terminal:
sed -i "s/os.getenv('MONGO_URI')/os.getenv('DEV_MONGO_URI')/" backend/dev/app.py

Step 2.2 â€” Update the production backend
sed -i "s/os.getenv('MONGO_URI')/os.getenv('PROD_MONGO_URI')/" backend/prod/app.py


Also disable Flask debug mode in production:
sed -i 's/debug=True/debug=False/' backend/prod/app.py

Step 2.3 â€” Fix the React API URLs
Replace frontend/src/pages/Tickets.js 

Phase 3 Create the three Dockerfiles
Step 3.1  Development backend Dockerfile
Step 3.2  Production backend Dockerfile
Step 3.3  Frontend Dockerfile
Step 3.4  Create Nginx configuration 

<img width="395" height="470" alt="image" src="https://github.com/user-attachments/assets/4ddfcbf0-8f38-4d6b-89f8-1de2bcbc62db" />

<img width="373" height="308" alt="image" src="https://github.com/user-attachments/assets/1c82b397-adf6-43dd-a65e-02c8f386012b" />

Phase 4 â€” Create Docker Compose
Create the file in your project root 

<img width="391" height="451" alt="image" src="https://github.com/user-attachments/assets/94ae561d-2028-4289-bd2e-bd8ce43e3448" />

<img width="385" height="349" alt="image" src="https://github.com/user-attachments/assets/c3cc93b2-e2b2-429a-82c8-21ed96d9c351" />

<img width="324" height="452" alt="image" src="https://github.com/user-attachments/assets/77df85da-cf6d-4751-ae83-92469decde05" />

<img width="316" height="394" alt="image" src="https://github.com/user-attachments/assets/280fc305-1ba8-494f-9c3c-460efbb87e6b" />

<img width="327" height="417" alt="image" src="https://github.com/user-attachments/assets/c25a4dce-74aa-41cc-a723-1e3debe86155" />


<img width="332" height="295" alt="image" src="https://github.com/user-attachments/assets/63411020-ff4b-4a85-a296-4495e7923ad1" />

<img width="321" height="294" alt="image" src="https://github.com/user-attachments/assets/c2c392e8-9cfe-4d3f-afbc-ada0c78d9a91" />

<img width="563" height="183" alt="image" src="https://github.com/user-attachments/assets/81faf51f-e559-4436-9ca0-bc1bcbf94677" />


Phase 5 â€” Validate configuration
Before building, run:
git status --short
docker compose config --quiet
grep -n "MONGO_URI" backend/dev/app.py backend/prod/app.py 

<img width="319" height="410" alt="image" src="https://github.com/user-attachments/assets/f9a767a1-4f2b-4fad-b46d-8a2092e5a827" />

<img width="330" height="361" alt="image" src="https://github.com/user-attachments/assets/0ab9f246-050f-4295-a744-4c3569e02997" />

Check that frontend no longer uses localhost:
grep -n "apiUrl" frontend/src/pages/Tickets.js

Phase 6 â€” Build and deploy
Run: docker compose up -d --build
docker compose ps
docker compose logs --tail=40

<img width="343" height="347" alt="image" src="https://github.com/user-attachments/assets/14f1a38a-32a3-4d75-aa43-5058d0b89e9a" />

<img width="310" height="408" alt="image" src="https://github.com/user-attachments/assets/9c45eb8f-8eef-4f00-9efb-b9b7362a45eb" /> 

<img width="317" height="150" alt="image" src="https://github.com/user-attachments/assets/4cafc241-a61d-4fc4-b79c-a212d7aed05d" /> 

<img width="403" height="537" alt="image" src="https://github.com/user-attachments/assets/48fa4685-3def-4ac8-a35e-68c9a80e7cd2" />



Step 1 â€” Create the development Dockerfile
Run this command in your EC2 Ubuntu terminal:

Step 2 â€” Verify all three Dockerfiles
Run:
ls -l backend/dev/Dockerfile
ls -l backend/prod/Dockerfile
ls -l frontend/Dockerfile 

<img width="390" height="273" alt="image" src="https://github.com/user-attachments/assets/c581790a-bf34-4b5b-bf07-0b5428e5c8bd" />


Step 3 â€” Verify the frontend configuration
ls -l frontend/nginx.conf

Step 4 â€” Build again
docker compose up -d --build

Step 5 â€” Check containers
If the build succeeds:
docker compose ps
docker compose logs --tail=30 

<img width="318" height="447" alt="image" src="https://github.com/user-attachments/assets/a0801588-d095-454a-8e51-a977ffbdaffd" />

<img width="311" height="408" alt="image" src="https://github.com/user-attachments/assets/e4f6d893-b550-4f92-b2fd-72f77487d33f" />

<img width="329" height="275" alt="image" src="https://github.com/user-attachments/assets/34f9051c-1c2f-417d-b998-e0aa973ccf06" /> 

<img width="539" height="164" alt="image" src="https://github.com/user-attachments/assets/bf777156-ec58-487b-8f52-36fdf240a999" />




Step 6 â€” Test the frontend from EC2
curl -I http://localhost:3000

<img width="374" height="240" alt="image" src="https://github.com/user-attachments/assets/78510dcb-6e08-4590-bf7d-1a4568757355" />



Step 1 â€” Check container status
In your EC2 Ubuntu terminal, run:
docker compose ps

<img width="884" height="146" alt="image" src="https://github.com/user-attachments/assets/74fce211-3db6-4bf0-95df-db3b8807e3e0" />




Step 2 â€” Test the frontend from EC2
curl -I http://localhost:3000

<img width="559" height="171" alt="image" src="https://github.com/user-attachments/assets/af2258e6-83ed-4402-9adc-d277661a1d15" />

<img width="382" height="455" alt="image" src="https://github.com/user-attachments/assets/94808596-6918-4482-a116-65099e8da68e" />

<img width="389" height="301" alt="image" src="https://github.com/user-attachments/assets/a0ba95cc-0ac7-4c28-a22b-139a409e8b91" />

<img width="335" height="233" alt="image" src="https://github.com/user-attachments/assets/559d2f62-d6b1-45a3-b80f-1df3ccf91b8a" />

Step 3 â€” Test the application in your browser
Open these URLs:
Application	URL
Home	http://3.89.62.29:3000
Development	http://3.89.62.29:3000/dev
Production	http://3.89.62.29:3000/prod


1. Home	http://3.89.62.29:3000 :

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1a7126d8-7fe8-42ad-8ce4-f165bbb0b8f0" />



2. Development	http://3.89.62.29:3000/dev:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/18e0e9e8-ebf2-4cb2-8384-3912a7b95d48" />


3. Production	http://3.89.62.29:3000/prod:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/71235aab-8186-494f-83d2-803ace0f1392" />


Step 3 â€” Test database connectivity
Run:
docker compose logs --tail=50 dev-backend prod-backend

<img width="383" height="519" alt="image" src="https://github.com/user-attachments/assets/12aab861-8fa3-4e03-b95e-9c78a78e06bc" />


Step 1 â€” Test the production API
Run this in your EC2 terminal:
curl -i http://localhost:3000/api/prod/tickets

<img width="689" height="250" alt="image" src="https://github.com/user-attachments/assets/f2ea971f-0816-4c7a-8e87-10d53c8a23ec" />




Step 2 â€” Refresh both browser pages
Open or refresh:
- Development environment
- Production environment


  
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/248b5bbe-b385-4c0a-a450-c2d64229f7e5" />


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4214b998-aeb2-48ac-a589-828bb54cb4e6" />



Step 1: Update Development backend
EC2 Ubuntu terminal

Open the file:
both app.py files in backend -> dev for prod and dev, and update the details.


<img width="644" height="166" alt="image" src="https://github.com/user-attachments/assets/92140131-310e-4925-81ae-250f8748b24f" />


---

## Deployment Evidence

The following screenshots demonstrate the successful AWS EC2 deployment, Docker containers, application pages, API responses, logs, and security configuration.

### 1. Application Home Page

![Application Home Page](Screenshots/Application%20home%20page.png)

### 2. Development Environment

![Developer Page](Screenshots/Developer%20page.png)

### 3. Development API Response

![Development API](Screenshots/Development%20API.png)

### 4. Docker Containers

![Docker Containers](Screenshots/Docker%20containers.png)

### 5. AWS EC2 Instance

![EC2 Running Instance](Screenshots/EC2%20running%20instance.png)

### 6. Application Logs

![Application Logs](Screenshots/Logs.png)

### 7. Production API Response

![Production API](Screenshots/Production%20API.png)

### 8. Security Group Inbound Rules

![Security Group Inbound Rules](Screenshots/Security%20group%20inbound%20rules.png)








