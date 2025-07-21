## 🛠️ DevOps CI/CD Flow Using Jenkins, Docker & Kubernetes with GitOps
##  Step📖 1. Summary
This project implements a complete CI/CD strategy using modern DevOps tools. It automates everything from code build and test to deployment in a Kubernetes environment using Jenkins, SonarQube, DockerHub, and Argo CD.

## Step🖼️ 2. System Architecture
Pipeline Steps:

Source code changes trigger a Jenkins job

Code is compiled and built with Maven

SonarQube evaluates the code quality

Tests are executed

Docker image is built and stored and artifact is created.

A deployment manifest is automatically updated

Argo CD applies the new deployment

## Step🧰 3. Stack of Tools
Component	Role:
Git	Codebase version control
Jenkins	Core CI/CD engine
        |
Maven	Builds the project
        |
SonarQube	Analyzes the code for bugs
        |
Docker	Builds and packages container images
        |
DockerHub	Registry for storing Docker images
        |
Argo CD	Deploys updates to Kubernetes via GitOps
        |
Kubernetes	Hosts the application

## Step🔁 4. Flow Description
Git push triggers Jenkins

Maven builds the application uisng pom.xml file

SonarQube scans the code

Jenkins runs unit tests

Docker image is created and uploaded to DockerHub

A script updates image tag in manifest Git repo

Argo CD detects changes and deploys to eks cluster

Failures trigger automated reports and notifications

## Step🔧 5. Jenkinsfile Overview
groovy code breif:
pipeline {
    agent any
    stages {
        stage('Compile') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Quality Analysis') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }
        stage('Testing') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Container Build') {
            steps {
                sh 'docker build -t myorg/app:${BUILD_NUMBER} .'
                sh 'docker push myorg/app:${BUILD_NUMBER}'
            }
        }
        stage('Manifest Update') {
            steps {
                sh './update-k8s-manifest.sh myorg/app:${BUILD_NUMBER}'
            }
        }
    }
}

## Step🔍 6. Code Quality & Tests
SonarQube gates based on code quality thresholds

Jenkins halts builds that fail quality checks or tests

Reports sent to dev team immediately on failure

## Step🧱 7. Docker Integration
Container images created only on passing builds

Tagged based on Git commit or Jenkins build number

DockerHub is used as the centralized image registry

## Step🚀 8. Argo CD Deployment
Create eks cluster using eksctl and point kubectl to it.
Clone rgocd, clone the file.

Image updater updates only the image tag

Argo CD watches the Git repo and applies changes

Rollback and manual sync available from Argo CD UI

## Step🔔 9. Build Notifications
Slack channel alerts for build/test failures

Email alerts configured for production pipeline

Detailed error logs included in reports

## Step⚙️ 10. Setting Up
Clone the project repo

Configure Jenkins, Maven, Docker, and SonarQube

Connect Jenkins to DockerHub

Create a separate Git repo for K8s manifests

Install and link Argo CD to the manifests repo

Trigger build by pushing code

📚 Helpful Links
Jenkins Pipeline

SonarQube Setup

DockerHub

Argo CD Docs

