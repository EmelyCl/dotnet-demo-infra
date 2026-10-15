pipeline {
    agent any

    stages {
        stage('Build .NET App') {
            agent {
                docker {
                    image 'mcr.microsoft.com/dotnet/sdk:10.0'
                    reuseNode true
                }
            }
            steps {
             dir('TodoApp') {
                    sh 'dotnet build'
                }
            }
        }
        stage('Deploy'){
            agent {
                docker {
                    image 'docker:cli'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                    reuseNode true
                }
            }
            steps {
                sh 'docker compose down'
                sh 'docker compose up -d --build'
            }
            post {
                failure {
                    sh 'docker compose logs todoappdb'
                }
            }
        }
    }
}