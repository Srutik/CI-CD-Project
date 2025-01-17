pipeline {
    agent any

    tools {
        nodejs 'Node16' // Use the Node.js version configured in Jenkins
    }

    environment {
        APP_NAME = 'basic-node-app'
        PORT = '3000'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Srutik/CI-CD-Project'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Artifacts') {
            steps {
                sh 'tar -czf ${APP_NAME}.tar.gz *'
                archiveArtifacts artifacts: "${APP_NAME}.tar.gz", fingerprint: true
            }
        }

        stage('Deploy to Server') {
            steps {
                // Example deployment script (SSH or other methods)
                sh '''
                scp ${APP_NAME}.tar.gz user@remote-server:/path/to/deploy
                ssh user@remote-server "cd /path/to/deploy && tar -xzf ${APP_NAME}.tar.gz && npm install && pm2 restart all"
                '''
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
