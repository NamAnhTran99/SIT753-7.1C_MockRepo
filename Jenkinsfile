pipeline {
    agent any
    environment {
        DIRECTORY_PATH = 'some/random/path'
        STAGING_ENVIRONMENT = 'Azure Staging'
        PRODUCTION_ENVIRONMENT = 'Azure Production'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Build ASP.NET application using dotnet build'
            }
        }
        stage('Unit & Integration Tests') {
            steps {
                echo 'Run unit and integration tests using xUnit and dotnet test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyze code quality using SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Perform security scan using OWASP Dependency-Check'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploy application to staging environment: ${env.STAGING_ENVIRONMENT} using Azure App Service"
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Run integration tests on staging using Postman/Newman'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploy application to production environment: ${env.PRODUCTION_ENVIRONMENT} using Azure App Service"
            }
        }
    }
    post {
        always {
            emailext(
         to: 'tnnamanh@gmail.com',
         subject: "Build ${currentBuild.currentResult}",
         body: "Pipeline finished with status: ${currentBuild.currentResult}"
      )
        }
    }
}
