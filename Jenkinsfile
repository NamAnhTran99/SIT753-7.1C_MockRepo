pipeline {
    agent any

    environment {
        DIRECTORY_PATH = 'some/random/path'
        STAGING_ENVIRONMENT = 'Azure Staging'
        PRODUCTION_ENVIRONMENT = 'Azure Production'
        EMAIL_TO = 'tnnamanh@gmail.com'
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
            post {
                always {
                    emailext(
                        to: "${env.EMAIL_TO}",
                        subject: "Test Stage ${currentBuild.currentResult}",
                        body: "Test stage finished with status: ${currentBuild.currentResult}",
                        attachLog: true
                    )
                }
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
            post {
                always {
                    emailext(
                        to: "${env.EMAIL_TO}",
                        subject: "Security Scan ${currentBuild.currentResult}",
                        body: "Security scan completed with status: ${currentBuild.currentResult}",
                        attachLog: true
                    )
                }
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

    // optional (you can keep or remove)
    post {
        always {
            emailext(
                to: "${env.EMAIL_TO}",
                subject: "Build ${currentBuild.currentResult}",
                body: "Pipeline finished with status: ${currentBuild.currentResult}",
                attachLog: true
            )
        }
    }
}