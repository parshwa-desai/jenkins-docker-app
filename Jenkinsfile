pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/<your-username>/jenkins-docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-docker-demo:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker rm -f jenkins-docker-container || true'
                sh 'docker run -d --name jenkins-docker-container -p 8085:80 jenkins-docker-demo:latest'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'curl -I http://localhost:8085 || true'
            }
        }
    }

    post {
        success {
            echo '✅ Docker pipeline executed successfully!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
