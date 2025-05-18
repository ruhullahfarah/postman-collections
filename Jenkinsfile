pipeline {
    agent any

    tools {
        nodejs 'node18'  // Must match the name you gave in Global Tool Configuration
    }

    stages {
        stage('Checkout Git') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/ruhullahfarah/postman-collections.git',
                credentialsId: 'github-token'
            }
        }

        stage('Run Postman Tests') {
            steps {
                bat 'npm install -g newman'
                bat 'newman run practiceAPI.postman_collection.json'
            }
        }
    }
}
