pipeline {
 agent any
 stages {
 stage('Clone Repository') {
 steps {
 git 'https://github.com/mohamadsolouki/MLOps.git'
 }
 }
 stage('Build Docker Image') {
 steps {
 sh 'docker build -t fraud-detector .'
 }
 }
 stage('Run Unit Tests') {
steps {
 sh 'docker run fraud-detector pytest tests/'
 }
 }
 stage('Push to Docker Registry') {
 steps {
 withDockerRegistry([credentialsId: 'docker-hub-credentials']) {
 sh 'docker tag fraud-detector mydockerhub/fraud-detector:latest'
 sh 'docker push mydockerhub/fraud-detector:latest'
 }
 }
 }
 stage('Deploy Model') {
steps {
 sh 'docker run -d -p 8000:8080 mydockerhub/fraud-detector:latest'
 }
 }
 }
 }