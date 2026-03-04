pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Run App') {
            steps {
                script {
                    sh 'pkill -f "node app.js" || true'
                    sh 'nohup node app.js > app.log 2>&1 &'
                    sleep 60
                    sh "curl http://localhost:${params.CUSTOM_PORT}" || echo "App is not responding!"
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
        }
    }
}
