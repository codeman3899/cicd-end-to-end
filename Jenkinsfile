pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/codeman3899/cicd-end-to-end.git',
                    branch: 'main'
            }
        }

        stage('Build Docker') {
            steps {
                sh '''
                    echo "Build Docker Image"
                    docker build -t xhazem043/cicd-e2e:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Push the artifacts') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh '''
                        echo "Login to Docker Hub"
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin

                        echo "Push to Docker Hub"
                        docker push xhazem043/cicd-e2e:${BUILD_NUMBER}

                        docker logout
                    '''
                }
            }
        }
    }
}
