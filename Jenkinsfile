pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                bat 'python -m pytest -v'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                bat 'python -m pip install pip-audit'
                bat 'python -m pip_audit'
            }
        }

        stage('Build Image') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t aws-jenkins-cicd:%BUILD_NUMBER% .'
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }

        failure {
            echo 'CI Pipeline failed!'
        }
    }
}