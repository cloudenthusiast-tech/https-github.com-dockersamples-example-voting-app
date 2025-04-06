pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/YOUR_USERNAME/example-voting-app.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    docker.build('voting-app-vote', './vote')
                    docker.build('voting-app-result', './result')
                    docker.build('voting-app-worker', './worker')
                }
            }
        }

        stage('Run App with Docker Compose') {
            steps {
                sh 'docker-compose up -d'
            }
        }

        stage('Smoke Test') {
            steps {
                sh 'curl http://localhost:5000'  // Hit the vote app
            }
        }
    }

    post {
        always {
            sh 'docker-compose down'
        }
    }
}
