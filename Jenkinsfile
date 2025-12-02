pipeline {
    agent any
    options {
        skipDefaultCheckout()
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nagasai31rgb/docker-image:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh """
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push nagasai31rgb/docker-image:latest
                    """
                }
            }
        }
    }
}
