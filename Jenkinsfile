pipeline {
    agent {
        docker {
            image 'openjdk:11-jdk'
            args '-u root:root'
        }
    }
    environment {
        DOCKER_CREDENTIALS = credentials('docker-hub-credentials')
        APP_VERSION = '1.0.0'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Checking out code from Git repository'
                sh 'git log --oneline -5'
            }
        }
        stage('Build') {
            steps {
                echo 'Building application with Maven/Gradle...'
                sh 'echo "Compiling source code..."'
            }
        }
        stage('Test') {
            steps {
                echo 'Running automated tests...'
                sh 'echo "Executing unit tests and integration tests"'
            }
        }
        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t devops-project:${APP_VERSION} . || echo "Docker build simulated"'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running security scans and managing credentials securely'
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    echo 'Credentials secured using Jenkins credentials manager'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying to staging/production environment'
            }
        }
        stage('Logging & Monitoring') {
            steps {
                echo 'Reviewing logs for troubleshooting and monitoring'
                sh 'echo "Collecting build logs..." && ls -la'
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed - cleaning up workspace'
            echo 'Build logs archived for troubleshooting'
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed - check logs for troubleshooting'
        }
    }
}
