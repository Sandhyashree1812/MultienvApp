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


