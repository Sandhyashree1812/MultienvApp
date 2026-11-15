# MultiEnv Ticket Management System

A full-stack application using Flask for both frontend and backend services, demonstrating environment-specific ticket management.

## Project Structure

```
multienv/
├── docker-compose.yml
├── backend/
│   ├── dev/
│   │   ├── app.py
│   │   ├── requirements.txt
│   │   ├── Dockerfile
│   │   └── .env
│   └── prod/
│       ├── app.py
│       ├── requirements.txt
│       ├── Dockerfile
│       └── .env
└── frontend/
    ├── app.py
    ├── requirements.txt
    ├── Dockerfile
    └── .env
```


Phase 1 – AWS EC2 infrastructure setup

Step 1. Launch an EC2 instance

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/080689e6-9dc9-4e76-8580-7f0c5bd9e9fb" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1becc349-ebc7-4f32-b8e8-bf579094d827" />

Phase 2 – Connect to EC2 using SSH

Run: ssh -i "$env:USERPROFILE\Downloads\multienv-key.pem" ubuntu@54.210.207.235

<img width="778" height="143" alt="image" src="https://github.com/user-attachments/assets/1672215d-2967-4e5d-bff4-62cb642f0aa2" /> 

<img width="873" height="320" alt="image" src="https://github.com/user-attachments/assets/c6fe2a11-2f42-4ec4-8875-e94704f7b651" />

<img width="755" height="241" alt="image" src="https://github.com/user-attachments/assets/747ee5f1-8bb1-4916-ac50-819f11283d3f" />


Phase 3 – Verify server resources

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

Phase 2 – Install Docker and Docker Compose

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

Step 1 — Clone the repository
git clone https://github.com/Sandhyashree1812/MultienvApp.git

Step 2 — Enter the project directory
cd MultienvApp

<img width="622" height="290" alt="image" src="https://github.com/user-attachments/assets/266baf07-4dc7-4fad-b577-03a2d2f6f597" />


Step 3 — Inspect the project structure
ls -la
find . -maxdepth 4 -type f | sort

Step 4 — Check available memory and disk space
free -h
df -h / 

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

2. Fix the React API URLs


3. Create the backend Dockerfiles
   frontend/src/pages/Tickets.js.
   Create the backend Dockerfiles
   Create backend/dev/Dockerfile
   Create backend/prod/Dockerfile

4. Create the frontend Dockerfile
Create frontend/Dockerfile
Create frontend/nginx.conf:


 . MangoDB:

 Step 1 — Create a new MongoDB Atlas project

 <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4adf0872-4838-4672-94bd-18766d89a3cb" /> 

 
 Step 2 — creating your MongoDB cluster

Step 3 — Choose Drivers and Client Libraries
Select Python as the driver.
- Language: Python
- Client Library: PyMongo (Synchronous)
Choose the recommended version if asked.

Copy the connection string
1. Find the Copy button beside the connection string.
2. Click it.
3. Paste it temporarily into Notepad on your computer.
4. Replace the username and password placeholders with your actual database user credentials.

Step 1 — Copy your connection string

Step 2 — Prepare two database URLs

We'll use the same cluster but separate databases.

Your development connection string should end with:
mongodb+srv://USERNAME:PASSWORD@YOUR_CLUSTER.mongodb.net/multienv_dev?retryWrites=true&w=majority
Your production connection string should end with:
mongodb+srv://USERNAME:PASSWORD@YOUR_CLUSTER.mongodb.net/multienv_prod?retryWrites=true&w=majority


Step 4 — Allow your EC2 server
This is important. Your EC2 server must be authorized separately.
1. In Atlas, open Security → Network Access.
2. Click Add IP Address : 54.210.207.235/32

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/31dfbc1b-58d1-4945-8806-4ba19c34fa88" /> 

In the Comment field, enter:
MultienvApp-EC2

Step 2 — Temporary access setting
You can leave this switch OFF.

That means the IP access entry won't automatically expire after six hours.

Step 3 — Confirm
Click the green Confirm button.

Step 4 — Verify database user
After confirming the IP:
1. Click Database Users in the left menu.
2. Check whether you already have a database user.

Step 1 — Create an application database user
Click + ADD NEW DATABASE USER at the top right.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/69572a19-b472-4079-9c50-43db334cc937" />


   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/62a85c57-718d-4483-91f1-58b4e1307c38" />


Step 1 — Assign the database role
In your second screenshot, the Built-in Role section shows 0 SELECTED.
1. Scroll slightly up in the user creation window.
2. Find Built-in Role.
3. Click Add Built In Role.
4. Open the role dropdown.
5. Select:
Select this role
Read and write to any database

Step 2 — Keep the other settings unchanged
- Custom Roles: Leave unchanged.
- Specific Privileges: Leave unchanged.
- Restrict Access to Specific Clusters: OFF.
- Temporary User: OFF.

  Step 3 — Create the user
Scroll to the bottom and click the green Add User button.

Configure MongoDB on your EC2 server
Step 1 — Get the connection string
1. Open Database → Clusters.
2. Find MultienvCluster.
3. Click Connect.
4. Select Drivers.
5. Choose Python and PyMongo.
6. Copy the connection string.

   Prepare the two database URLs
We'll use separate databases:
- multienv_dev
- multienv_prod

  Step 3 — Create the environment file on EC2
Return to your Ubuntu SSH terminal and run:







## Environment Configuration

### Backend Development Environment (.env)
```
PORT=3001
MONGO_URI=your_dev_mongodb_uri
```

### Backend Production Environment (.env)
```
PORT=3002
MONGO_URI=your_prod_mongodb_uri
```



### Requirements
```
flask==2.0.1
flask-cors==3.0.10
python-dotenv==0.19.0
pymongo==3.12.0
requests==2.26.0
```



### Using Docker Compose
```bash
docker-compose up
```

## Accessing the Application

- Frontend: http://localhost:3000/
- Development Environment: http://localhost:3001/dev
- Production Environment: http://localhost:3002/prod



## Security Considerations

- Never commit `.env` files to version control
- Use different MongoDB databases for dev and prod
- Implement proper authentication
- Use secure headers


