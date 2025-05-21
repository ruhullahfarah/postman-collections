pipeline {
    agent any

    tools {
        nodejs 'node18'
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
                bat 'npm install newman newman-reporter-html'
            }
        }

        stage('Run Postman Tests') {
            steps {
                bat '''
                    npx newman run practiceAPI.postman_collection.json ^
                      -e practiceAPI-env.postman_environment.json ^
                      --reporters cli,junit,html ^
                      --reporter-junit-export results.xml ^
                      --reporter-html-export newman-report.html
                '''
            }
        }
    }

    post {
        always {
            // Publish JUnit report
            junit 'results.xml'

            // Publish HTML report (requires "HTML Publisher" plugin)
            publishHTML(target: [
                reportDir: '.',                // Current workspace
                reportFiles: 'newman-report.html',
                reportName: 'Newman HTML Report',
                keepAll: true,
                alwaysLinkToLastBuild: true,
                allowMissing: false
            ])
        }
    }
}
