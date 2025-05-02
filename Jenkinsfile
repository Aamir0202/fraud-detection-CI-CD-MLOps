pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t fraud-detector .'
            }
        }

        stage('Push to Docker Registry') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    bat 'docker tag fraud-detector aamir0202/fraud-detector:latest'
                    bat 'docker push aamir0202/fraud-detector:latest'
                }
            }
        }

        stage('Deploy Model') {
            steps {
                bat 'docker run -d -p 5002:8080 aamir0202/fraud-detector:latest'
            }
        }
    }
}
