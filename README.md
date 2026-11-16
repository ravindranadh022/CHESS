# CHESS
# Chess AI Project

An AI-powered chess game using Python with `python-chess` for game logic and `Pygame` for the GUI.

## Setup Instructions

1. Install Python 3.8 or higher
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Project Structure

- `chess_ai.py` - Main AI engine with Minimax algorithm
- `chess_gui.py` - Pygame-based graphical interface
- `main.py` - Game loop and integration

## How to Run

```bash
python main.py
```

## Features

- Complete chess rules implementation (castling, en passant, pawn promotion)
- AI using Minimax with Alpha-Beta pruning
- Interactive GUI with drag-and-drop piece movement
- Move validation and game state detection (check, checkmate, stalemate)




























































































































git --version
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
git config --global user.name
git config --global user.email
git init
git status
git add .
git add filename
git commit -m "first commit"
git log
git log --oneline
git log --oneline --all --decorate
git branch
git branch feature
git checkout feature
git checkout main
git checkout -b feature
git merge feature
git revert <commit-hash>
git stash
git stash -u
git stash list
git stash pop
git restore filename
git diff
git diff --staged
git remote -v
git remote add origin https://github.com/YOUR_USERNAME/REPOSITORY.git
git remote set-url origin https://github.com/YOUR_USERNAME/REPOSITORY.git
git branch -M main
git push -u origin main
git push
git pull
git fetch
git clone https://github.com/USERNAME/REPOSITORY.git
git rm filename
git mv oldname newname







STEP 1: Create a GitHub Repository
We are using our existing Maven web application.

GitHub Repository:

https://github.com/ravindranadh022/mw.git

No need to create another repository.
STEP 2: Create an AWS EC2 Instance
Execute: AWS Management Console (Browser)
1. Login to AWS.
2. Search for EC2.
3. Click Launch Instance.
4. Configure the following:
Configuration	Value
Name	cloud-deployment
AMI	Ubuntu Server 24.04 LTS
Architecture	64-bit x86
Instance Type	Free-tier-eligible micro instance
Key Pair	Create new key pair
Key Name	cloud-deployment
Key Format	.pem
Storage	8 GiB


5. Create a Security Group.
Configure inbound rules
Type	Port	Source
SSH	22	My IP
HTTP	80	Anywhere
HTTPS	443	Anywhere


6. Enable Auto-assign Public IP.
7. Click Launch Instance.
Wait until the instance state becomes Running.
STEP 3: Connect to Ubuntu using SSH
Execute: Windows PowerShell

First, move your .pem file into your AWS folder.

Navigate to that folder:
cd C:\Users\ravin\OneDrive\Desktop\AWS

Open AWS EC2 → Instances → Select your instance → Connect → SSH Client.

Copy the SSH command provided by AWS.

It will look similar to:
ssh -i "cloud-deployment.pem" ubuntu@YOUR_PUBLIC_IP

If prompted:
Are you sure you want to continue connecting?

Type:
yes

Expected output
ubuntu@ip-172-31-xx-xx:~$

You are now connected to the Ubuntu cloud machine.

Important: All subsequent commands are executed inside the Ubuntu terminal unless specified otherwise.
STEP 4: Install Required Software
Execute: Ubuntu EC2 Terminal
sudo apt update

sudo apt install -y docker.io git nano openjdk-17-jdk maven

sudo systemctl enable docker

sudo systemctl start docker

sudo usermod -aG docker ubuntu

newgrp docker

Verify installations
docker --version

git --version

java -version

mvn -version

Test Docker
docker run hello-world

Expected output:
Hello from Docker!
This message shows that your installation appears to be working correctly.

STEP 5: Clone the Application from GitHub
Execute: Ubuntu EC2 Terminal
git clone https://github.com/ravindranadh022/mw.git

cd mw

Check project files:
ls

You should find:
pom.xml
src
Dockerfile

STEP 6: Build the Maven Application
Execute: Ubuntu EC2 Terminal (inside mw folder)
mvn clean package

This command:
- clean removes previous build files.
- package compiles the application and generates the WAR file.
Check the generated WAR file:
ls target

Expected output:
maven-archiver
maven-web-project1
maven-web-project1.war

STEP 7: Create the Dockerfile
Execute: Ubuntu EC2 Terminal (inside mw folder)

Check whether Dockerfile already exists:
cat Dockerfile

Our existing Dockerfile:
FROM tomcat:9.0

COPY target/maven-web-project1.war /usr/local/tomcat/webapps/maven-web-project1.war

Explanation:
Instruction	Purpose
FROM	Downloads Tomcat 9.0 base image
COPY	Copies WAR file into Tomcat webapps directory


No need to create another Dockerfile because our GitHub repository already contains it.
STEP 8: Build the Docker Image
Execute: Ubuntu EC2 Terminal (inside mw folder)
docker build -t cloud-web-app .

Explanation:
- docker build – Builds an image.
- -t – Assigns a name.
- cloud-web-app – Image name.
- . – Current directory.
Verify Docker Image
docker images

Expected output:
REPOSITORY       TAG
cloud-web-app    latest
tomcat           9.0

STEP 9: Run the Docker Container
Execute: Ubuntu EC2 Terminal
docker run -d --name cloud-web-container -p 6060:8080 cloud-web-app

Explanation:
Command	Purpose
docker run	Creates and runs a container
-d	Runs in background
--name	Assigns container name
-p 6060:8080	Maps host port 6060 to container port 8080
cloud-web-app	Docker image name


Check running containers
docker ps

You should see:
cloud-web-container
0.0.0.0:6060->8080/tcp

Test the application locally
curl http://localhost:6060/maven-web-project1/

If HTML output appears, the application is running.
STEP 10: Configure AWS Security Group
Execute: AWS Management Console (Browser)
1. Open EC2.
2. Select cloud-deployment.
3. Open the Security tab.
4. Click the associated Security Group.
5. Select Inbound Rules.
6. Click Edit Inbound Rules.
7. Add the following rule:
Type	Protocol	Port	Source
Custom TCP	TCP	6060	0.0.0.0/0


8. Click Save Rules.
This allows users to access our application through port 6060.
STEP 11: Access the Application Publicly
Execute: Windows Browser

Go to AWS EC2 and copy the Public IPv4 address.

Open:
http://YOUR_PUBLIC_IP:6060/maven-web-project1/

For our completed practical, the URL was:
http://54.226.18.53:6060/maven-web-project1/

Expected output:
Hello World!

Hello from Maven Web Project!

This web application is running on Apache Tomcat.

Congratulations! Your application is successfully deployed into the AWS Cloud.
STEP 12: Stop the EC2 Instance
Execute: AWS Management Console (Browser)
1. Open EC2 → Instances.
2. Select cloud-deployment.
3. Click Instance State.
4. Select Stop Instance.
5. Confirm.
Wait until the status becomes:
Stopped

Note: Stopping preserves your application files and installed software. EBS storage charges may continue. The public IP may change when you restart the instance.
COMPLETE COMMANDS – COPY SECTION
Here are all the Ubuntu commands in one place, in execution order.

These commands assume you have already connected to EC2 using SSH.

Execute everything below in Ubuntu EC2 Terminal.
sudo apt update

sudo apt install -y docker.io git nano openjdk-17-jdk maven

sudo systemctl enable docker

sudo systemctl start docker

sudo usermod -aG docker ubuntu

newgrp docker

docker --version
git --version
java -version
mvn -version

docker run hello-world

git clone https://github.com/ravindranadh022/mw.git

cd mw

ls

mvn clean package

ls target

cat Dockerfile

docker build -t cloud-web-app .

docker images

docker run -d --name cloud-web-container -p 6060:8080 cloud-web-app

docker ps

curl http://localhost:6060/maven-web-project1/

Remember: The AWS Security Group configuration and browser access are performed separately through the AWS Console and your browser.
IMPORTANT: 10 Scenario-Based Examination Questions
Your reference document contains these questions on pages 9–11. Learn these answers.
No.	Question	Answer
1	EC2 is running, but the public IP doesn't display index.html. What should you do?	Install Apache, place index.html in the web root, start Apache and configure Security Group.
2	Webpage isn't loading even after placing index.html in /var/www/html/. What will you check?	Security Group and Apache Service.
3	Apache stops after instance reboot. What command ensures automatic startup?	sudo systemctl enable apache2
4	How do you install Maven on Ubuntu EC2?	sudo apt update followed by sudo apt install maven -y
5	Where should you place a WAR file for Tomcat deployment?	Tomcat's webapps directory.
6	Maven application gives 404 error. What should you check?	Context Path, WAR Filename and Tomcat Logs.
7	Application works using localhost:8080 but not in browser. What is missing?	Security Group inbound TCP port 8080.
8	Public IP changes after restarting EC2. What feature prevents this?	Elastic IP.
9	Which EC2 feature executes commands automatically during instance setup?	EC2 User Data.
10	EC2 has no internet to download Maven dependencies. What AWS service can provide internet access from a private subnet?	NAT Gateway.


Note: For Scenario 1, the Apache installation and service commands depend on the OS. Ubuntu uses apache2; Amazon Linux 2 uses httpd. The table's Scenario 5 follows the reference's Tomcat deployment concept; the exact directory can vary by Tomcat installation.
Final Revision: Remember This Workflow!
Memorize these five main steps:

1. Create application and push into GitHub.

2. Create EC2 instance and connect to Ubuntu.

3. Clone application and write Dockerfile.

4. Create Docker image.

5. Run Docker image and access application using public IP.

These are the five major steps explicitly listed in your reference document.

You have now completed the entire practical successfully! 🎯
