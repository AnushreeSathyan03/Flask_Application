pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/AnushreeSathyan03/Flask_Application.git'
            }
        }

        stage('Set up Virtual Environment') {
            steps {
                bat 'python -m venv venv'
                bat '.\\venv\\Scripts\\activate'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '.\\venv\\Scripts\\activate && pip install -r requirements.txt'
            }
        }

        stage('Run Flask App') {
            steps {
                bat '.\\venv\\Scripts\\activate && start /B python app.py'
                sleep 10  // Wait for Flask to fully start
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'curl http://127.0.0.1:5000'
            }
        }
    }

    post {
        success {
            echo '🎉 Deployment successful!'
        }
        failure {
            echo '🚨 Deployment failed!'
        }
    }
}
