pipeline {
    agent any 
    stages {
        stage('Preparation') {
            steps {
                catchError(buildResult: 'SUCCESS') {
                    sh 'docker stop todoappdb'
                    sh 'docker rm todoappdb'
                }
            }
        }
    
        stage('Build') {
            steps{
                sh 'docker compose up -d --build'
            }
        }
    } 
}