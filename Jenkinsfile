pipeline {
    agent any

    tools {
        nodejs 'Node16' // Use the Node.js version configured in Jenkins
    }

    environment {
        APP_NAME = 'basic-node-app'
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
                // Create a zip artifact containing all project files
                sh 'zip -r ${APP_NAME}.zip *'
                archiveArtifacts artifacts: "${APP_NAME}.zip", fingerprint: true
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
