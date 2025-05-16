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
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
            post {
                always {
                    
                    emailext (
                        subject: "Jenkins Build - Run Tests Stage - ${currentBuild.currentResult}",
                        body: """\
                            <p>Run Tests stage completed with status: ${currentBuild.currentResult}</p>
                            <p>Check the Jenkins console output for details.</p>
                        """,
                        to: 's223987254@deakin.edu.au',
                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
            post {
                always {
                    
                    emailext (
                        subject: "Jenkins Build - Security Scan Stage - ${currentBuild.currentResult}",
                        body: """\
                            <p>Security scan stage completed with status: ${currentBuild.currentResult}</p>
                            <p>Check the Jenkins console output for details.</p>
                        """,
                        to: 's223987254@deakin.edu.au',
                        attachLog: true
                    )
                }
            }
        }
    }
}
