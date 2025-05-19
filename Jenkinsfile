pipeline {
    agent any
    tools {
        nodejs "node18"  // Name as defined in Jenkins Global Tools Configuration
    }
    environment {
        PATH = "${tool 'node18'}/bin:${env.PATH}"
    }
    stages {
        stage('Checkout Git') {
            steps {
                git url: 'https://github.com/ruhullahfarah/postman-collections.git', branch: 'main', credentialsId: 'github-token'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install newman'
            }
        }
        stage('Run Postman Tests') {
            steps {
                bat 'npx newman run practiceAPI.postman_collection.json'
            }
        }
    }
}
