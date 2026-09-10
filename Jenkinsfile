pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building application...'

                sh '''
                    python3 -m venv venv
                    venv/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'

                sh '''
                    venv/bin/python -m py_compile app.py
                '''
            }
        }

    }
}
