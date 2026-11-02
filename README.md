# Jenkins CI/CD Pipeline Project

## Overview
Complete Jenkins automation server with declarative pipeline, Docker integration, and security.

## 1. Environment Setup
Install Jenkins on Ubuntu EC2/VM:
sudo apt update && sudo apt install openjdk-11-jdk -y
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update && sudo apt install jenkins -y
sudo systemctl start jenkins
Initial password: sudo cat /var/lib/jenkins/secrets/initialAdminPassword

## 2. Repository Integration
GitHub repo: https://github.com/kasimuhussaini901-glitch/devops-project
Webhook: http://JENKINS_URL/github-webhook/
Poll SCM: H/5 * * * *

## 3. Job Configuration
New Item > Pipeline > Pipeline script from SCM > Git URL > Branch main > Jenkinsfile

## 4. Declarative Pipeline
pipeline { agent { docker { image 'openjdk:11-jdk' } } environment { } stages { Checkout, Build, Test, Docker Build, Security Scan, Deploy, Logging } post { } }

## 5. Docker Integration
Docker agent, docker build stage, Dockerfile present.

## 6. Security
Credentials stored in Jenkins Credentials Manager: docker-hub-credentials, used via credentials() and withCredentials.

## 7. Troubleshooting
Check Console Output, Docker Pipeline plugin, credential ID, logs archived.
