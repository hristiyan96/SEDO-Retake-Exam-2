pipeline {
    agent any

    environment {
        DOTNET_VERSION = "8.0"
    }

    triggers {
        pollSCM('* * * * *') // Optional: check for changes in main branch every minute
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/hristiyan96/SEDO-Retake-Exam-2.git'
            }
        }

        stage('Restore Dependencies') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build --configuration Release'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'dotnet test --configuration Release --no-build'
            }
        }
    }

    post {
        always {
            cleanWs() // Clean workspace after every run
        }
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed!'
        }
    }
}
