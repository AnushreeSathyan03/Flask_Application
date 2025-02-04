pipeline {
    agent any

    environment {
        VENV_DIR = 'venv'
        FLASK_APP = 'app.py'
        REPO_URL = 'https://github.com/AnushreeSathyan03/Flask_Application.git'
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    git url: REPO_URL
                }
            }
        }

        stage('Set up Virtual Environment') {
            steps {
                script {
                    bat '''
                    python -m venv venv
                    .\\venv\\Scripts\\activate
                    '''
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    bat '''
                    .\\venv\\Scripts\\activate
                    pip install -r requirements.txt
                    '''
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    bat '''
                    .\\venv\\Scripts\\activate
                    pytest > test_results.log
                    '''
                }
            }
        }

        stage('Start Gunicorn Server') {
            steps {
                script {
                    bat '''
                    .\\venv\\Scripts\\activate
                    gunicorn -b 127.0.0.1:8000 app:app
                    '''
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    bat '''
                    curl http://127.0.0.1:5000
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
