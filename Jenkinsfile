stage('Checkout'){
    steps {
        git url: 'https://github.com/codeman3899/cicd-end-to-end.git',
            branch: 'main'
    }
}

stage('Build Docker'){
    steps{
        script{
            sh '''
            echo 'Buid Docker Image'
            docker build -t xhazem043/cicd-e2e:${BUILD_NUMBER} .
            '''
        }
    }
}

stage('Push the artifacts'){
    steps{
        script{
            sh '''
            echo 'Push to Repo'
            docker push xhazem043/cicd-e2e:${BUILD_NUMBER}
            '''
        }
    }
}
