pipeline {
    agent any
    stages {
        stage('Checkout Git') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/ruhullahfarah/api-tests.git'
            }
        }
        stage('Run Postman Tests') {
            steps {
                bat 'npm install -g newman'  // Installs Newman
                bat 'newman run practiceAPI.postman_collection.json'  // Runs tests
            }
        }
    }
}