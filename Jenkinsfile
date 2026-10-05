node {
    stage('Preparation') {
        catchError(buildResult: 'SUCCESS') {
            sh 'docker stop todoappdb'
            sh 'docker rm todoappdb'
        }
    }
    stage('Database') {
        sh 'docker pull mariadb:11'
        sh 'docker volume create mariadb-data'
        sh 'docker run -d --name todoappdb -p 3306:3306 -e MARIADB_ROOT_PASSWORD=sekrit -e MARIADB_DATABASE=todo_db -e MARIADB_USER=todo_usr -e MARIADB_PASSWORD=letmeinplz -v mariadb-data:/var/lib/mysql:Z mariadb:11'
    }
        stage('Build') {
            dir('TodoApp') {
            sh 'docker run --rm -v ${WORKSPACE}:/app -w /app mcr.microsoft.com/dotnet/sdk:10.0 dotnet build TodoApp'
        }
    }
} 