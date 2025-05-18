pipeline {
    agent any
    stages {
        stage('Checkout Git') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/ruhullahfarah/postman-collections.git',
                credentialsId: 'github-token'  // Ensure this matches your Jenkins credential ID
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