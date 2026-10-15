pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('hind105/my-app')
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
                        docker.image('hind105/my-app').push('latest')
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker rm -f my-app || true'
                sh 'docker run -d --name my-app -p 3000:3000 hind105/my-app:latest'
            }
        }
    }
}