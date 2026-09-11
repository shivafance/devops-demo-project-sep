pipeline {
agent any


stages {

    stage('Build') {
        steps {
            sh 'python3 -m venv venv'
            sh 'venv/bin/pip install -r requirements.txt'
        }
    }

    stage('Test') {
        steps {
            sh 'venv/bin/python -m py_compile app.py'
        }
    }

    stage('Docker Build') {
        steps {
            sh 'docker build -t devops-demo-app:jenkins .'
        }
    }

    stage('Docker Push') {
        steps {
            withCredentials([usernamePassword(
                credentialsId: 'dockerhub-credentials',
                usernameVariable: 'DOCKER_USERNAME',
                passwordVariable: 'DOCKER_PASSWORD'
            )]) {
                sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'
                sh 'docker tag devops-demo-app:jenkins $DOCKER_USERNAME/devops-demo-app:jenkins'
                sh 'docker push $DOCKER_USERNAME/devops-demo-app:jenkins'
                sh 'docker logout'
            }
        }
    }
}


}

