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
                sh '''
cat > docker-compose.jenkins.yml <<'EOF'
services:
  todoapp:
    ports:
      - "8081:8080"
EOF
'''
                sh 'docker compose -f docker-compose.yml -f docker-compose.jenkins.yml config -q'
                sh 'docker compose -f docker-compose.yml -f docker-compose.jenkins.yml down'
                sh 'docker compose -f docker-compose.yml -f docker-compose.jenkins.yml up -d --build'
            }
        }
    }
}