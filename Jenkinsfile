node {
    stage('Preparation') {
        catchError(buildResult: 'SUCCESS') {
            sh 'docker stop todoappdb'
            sh 'docker rm todoappdb'
        }
    }
  
    stage('Build') {
        sh 'dotnet restore' 
        sh 'dotnet build --no-restore'
    }
} 