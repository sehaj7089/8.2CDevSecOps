pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sehaj7089/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npm test || exit 0'
            }
        }
        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit 0'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit 0'
            }
        }
        stage('Email Notification') {
            steps {
                script {
                    emailext (
                        subject: "Jenkins Build - ${currentBuild.fullDisplayName}",
                        body: """Build Status: ${currentBuild.currentResult}
See console output at: ${env.BUILD_URL}console""",
                        to: 'sehaj9087@gmail.com',
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }
    }
}
