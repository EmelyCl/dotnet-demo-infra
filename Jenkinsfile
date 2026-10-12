pipeline {
    agent any

    stages {
        stage('Build .NET App') {
            agent {
                docker {
                    image 'mcr.microsoft.com/dotnet/sdk:10.0'
                }
            }
            steps {
             dir('TodoApp') {
                    sh 'dotnet run'
                }
            }
        }
    }
}