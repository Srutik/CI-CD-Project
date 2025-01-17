pipeline {
    agent any

    stages {
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
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*', fingerprint: true
            }
        }
        stage('Deploy to Azure') {
            steps {
                sh '''
                az login --service-principal -u $SP_USER -p $SP_PASS --tenant $TENANT_ID
                az webapp deploy --resource-group $RESOURCE_GROUP --name $APP_NAME --src-path .
                '''
            }
        }
    }
}
