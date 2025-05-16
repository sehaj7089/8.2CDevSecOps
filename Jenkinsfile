pipeline {
    agent any

    environment {
        SNYK_TOKEN = credentials('snyk-token') 
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true' 
            }
        }

        stage('Snyk Security Scan') {
            steps {
                sh 'npm install -g snyk'
                sh 'snyk auth $SNYK_TOKEN'
                sh 'snyk test'
            }
        }
    }
}

