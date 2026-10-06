pipeline {
    agent any //{
    //     docker {
    //         image 'mcr.microsoft.com/dotnet/sdk:10.0'
    //     }
    // }
    
    stage('Preparation') {
        catchError(buildResult: 'SUCCESS') {
            sh 'docker stop todoappdb'
            sh 'docker rm todoappdb'
        }
    }
  
    stage('Build') {
        sh 'docker compose up -d --build'
    }
} 