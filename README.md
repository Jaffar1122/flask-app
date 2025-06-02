# Flask Docker CI/CD Pipeline with Jenkins

This project demonstrates a **CI/CD pipeline** for a simple Flask application using **Docker** and **Jenkins**.  
It shows how to automate building a Docker image, running a container, and deploying via Jenkins pipeline.

---

## Project Overview

- Flask app serving a basic web page on port 5000  
- Dockerized Flask app with a Dockerfile  
- Jenkins pipeline to clone repo, build Docker image, and run the container  
- Automated builds to streamline deployment  
- Ideal for showcasing practical DevOps skills with Jenkins and Docker

---

## Features

- Git integration: Clones code from GitHub  
- Docker build: Creates a Docker image from the Flask app  
- Container run: Runs the app inside a Docker container  
- Pipeline stages: Clone → Build → Run with clear Jenkins pipeline syntax  
- Handles Docker permissions for Jenkins user  
- Simple, easy to understand, and extensible

---

## Prerequisites

- Jenkins installed on a Linux server with Docker  
- Jenkins user added to `docker` group to access Docker daemon  
- Git installed on Jenkins machine  
- Docker daemon running and accessible  
- Basic knowledge of Jenkins pipelines and Docker commands

---

## Jenkins Pipeline Script

```groovy
pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Jaffar1122/flask-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('flask-app')
                }
            }
        }
        stage('Run Container') {
            steps {
                script {
                    sh 'docker rm -f flask-app || true'
                    docker.image('flask-app').run('-d -p 5000:5000 --name flask-app')
                }
            }
        }
    }
}
How to Run
Clone this repo to Jenkins workspace

Create a Jenkins pipeline job and paste the above script

Ensure Jenkins user has Docker permissions:

bash
Copy
Edit
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
Run the Jenkins pipeline job

Visit http://<JENKINS_SERVER_IP>:5000 to see the Flask app running in Docker container

Notes
Port 5000 is used by Flask app inside the Docker container, mapped to host port 5000

Make sure no other service is using port 5000 on your Jenkins server

You can add webhook triggers in GitHub to automatically start builds on commits (optional)


My result🚀 
https://1drv.ms/i/c/79020f308116c3bc/EQWa0tLYvixDiY_dUj9MLC8BwuiUDvfZBRM5965Yi7e5wg?e=35mRCr


Author
Jaffar Hussain

License
MIT License

Feel free to explore and modify the pipeline for your own projects!

yaml
Copy
Edit

---

#
