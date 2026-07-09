pipeline {

    agent any

    environment {

        IMAGE_NAME = "divyaerupaka/docker-demo"

    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/DivyaErupaka/docker-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Docker Login') {

            steps {

                withCredentials([
                    usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                    )
                ]) {

                    sh '''
                    echo $DOCKER_PASS | docker login \
                    -u $DOCKER_USER \
                    --password-stdin
                    '''
                }
            }
        }

        stage('Push Image') {

            steps {

                sh 'docker push $IMAGE_NAME:latest'

            }

        }

    }

}
