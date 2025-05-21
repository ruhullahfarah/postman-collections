pipeline {
    agent any

    tools {
        nodejs 'node18'  // Name must match the one in Jenkins > Global Tool Configuration
    }

    environment {
        PATH = "${tool 'node18'}/bin;${env.PATH}"
    }

    stages {
        stage('Checkout Git') {
            steps {
                git url: 'https://github.com/ruhullahfarah/postman-collections.git',
                    branch: 'main',
                    credentialsId: 'github-token'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm ci --no-audit --no-fund'
                bat 'npm install newman newman-reporter-htmlextra'
            }
        }

        stage('Run Postman Tests') {
            steps {
                bat '''
                    npx newman run practiceAPI.postman_collection.json ^
                      --reporters cli,junit,htmlextra ^
                      --reporter-junit-export results.xml ^
                      --reporter-htmlextra-export newman-report.html
                '''
            }
        }
    }

    post {
        always {
            junit 'results.xml'

            publishHTML(target: [
                reportDir: '.',                       // Current workspace
                reportFiles: 'newman-report.html',
                reportName: 'Newman HTML Report',
                keepAll: true,
                alwaysLinkToLastBuild: true,
                allowMissing: false
            ])
        }
    }
}
