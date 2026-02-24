# Flask + Nginx Production-Style Deployment

This project demonstrates a simple production-style backend deployment using Flask and Nginx inside Docker on an AWS EC2 instance.

The goal was to understand how real-world containerized applications are structured and deployed.

---

## Tech Stack

- Flask (Backend Application)
- Nginx (Reverse Proxy)
- Docker
- Custom Docker Network
- Named Volume
- GitHub (SSH-based workflow)
- AWS EC2 (Ubuntu)

---

## Architecture

Client → Nginx (Port 80) → Flask Backend (Internal Docker Network)

- The Flask app is NOT exposed directly to the internet.
- Nginx acts as a reverse proxy.
- Containers communicate using a custom Docker network.
- A named Docker volume is used for container storage.
- Only port 80 is exposed publicly.

---

##  How to Run

### 1️⃣ Build the Docker image

docker build -t flask-prod .

### 2️⃣ Create a custom Docker network

docker network create prod-network

### 3️⃣ Run the Flask backend (internal only)

docker run -d \
--name backend \
--network prod-network \
flask-prod

### 4️⃣ Run Nginx (reverse proxy)

docker run -d \
--name nginx \
--network prod-network \
-p 80:80 \
-v $(pwd)/nginx/default.conf:/etc/nginx/conf.d/default.conf \
nginx

Now access the application using:

http://<your-ec2-public-ip>

---

## 📚 What I Practiced

- Creating optimized Docker images
- Understanding Docker layer caching
- Configuring Nginx as a reverse proxy
- Working with custom Docker networks
- Using named volumes
- Debugging container issues
- Deploying via GitHub SSH workflow
- Running applications on AWS EC2

---

This project helped me understand how containerized backend services are structured and deployed in a production-style environment.
