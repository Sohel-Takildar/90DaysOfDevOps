# Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

## Objective

Today I deployed a real cloud server, connected using SSH, installed Docker and Nginx, configured firewall/security group rules, and verified the web server was accessible from the internet.

---

# Cloud Provider Used

* AWS EC2 (Ubuntu 24.04 LTS)

---

# Part 1 – Launch Cloud Instance & SSH Access

## Steps Performed

### 1. Created EC2 Instance

* Logged into AWS Console
* Navigated to EC2 Dashboard
* Launched a new Ubuntu instance
* Selected Free Tier eligible instance type (`t2.micro`)
* Created and downloaded SSH key pair (`my-key.pem`)

### 2. Configured Security Group

Allowed the following inbound rules:

| Type | Protocol | Port |
| ---- | -------- | ---- |
| SSH  | TCP      | 22   |
| HTTP | TCP      | 80   |

### 3. Connected to Server Using SSH

```bash
chmod 400 my-key.pem

ssh -i my-key.pem ubuntu@<your-public-ip>
```

Successfully connected to the server.

---

# Part 2 – Install Docker & Nginx

## Step 1 – Update System

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Step 2 – Install Docker

```bash
sudo apt install docker.io -y
```

### Verify Docker Installation

```bash
docker --version
```

### Start and Enable Docker

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### Verify Docker Service

```bash
sudo systemctl status docker
```

---

## Step 3 – Install Nginx

```bash
sudo apt install nginx -y
```

### Start and Enable Nginx

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

### Verify Nginx Status

```bash
sudo systemctl status nginx
```

---

# Part 3 – Security Group Configuration

After allowing HTTP (Port 80) in the EC2 Security Group, I opened the browser and visited:

```bash
http://<your-public-ip>
```

The Nginx welcome page loaded successfully.

---

# Part 4 – Extract Nginx Logs

## View Nginx Access Logs

```bash
sudo cat /var/log/nginx/access.log
```

## Save Logs to File

```bash
sudo cp /var/log/nginx/access.log ~/nginx-logs.txt
```

## Download Log File to Local Machine

```bash
scp -i my-key.pem ubuntu@<your-public-ip>:~/nginx-logs.txt .
```

The log file was downloaded successfully.

---

# Commands Used

```bash
ssh -i my-key.pem ubuntu@<your-public-ip>

sudo apt update && sudo apt upgrade -y

sudo apt install docker.io -y

docker --version

sudo systemctl start docker
sudo systemctl enable docker
sudo systemctl status docker

sudo apt install nginx -y

sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx

sudo cat /var/log/nginx/access.log

sudo cp /var/log/nginx/access.log ~/nginx-logs.txt

scp -i my-key.pem ubuntu@<your-public-ip>:~/nginx-logs.txt .
```

---

# Challenges Faced

## 1. Permission Denied While SSH

Initially received:

```bash
Permission denied (publickey)
```

### Solution

Changed the key permission:

```bash
chmod 400 my-key.pem
```

---

## 2. Nginx Page Not Loading

The browser could not access the server.

### Solution

Added HTTP port 80 rule in AWS Security Group.

---

## 3. Docker Service Not Running

Docker service was inactive after installation.

### Solution

```bash
sudo systemctl start docker
```

Then enabled it permanently:

```bash
sudo systemctl enable docker
```

---

# What I Learned

* How to launch and configure a cloud server
* How SSH authentication works using PEM keys
* How to install and manage services using systemctl
* How security groups control server access
* How to access and extract server logs
* Basic cloud troubleshooting and deployment workflow

---
