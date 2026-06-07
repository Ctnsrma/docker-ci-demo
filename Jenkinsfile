pipeline{
    agent any 
    stages {
        stage('Build Docker Image'){
            steps{
                bat 'docker build -t ctnsrma/docker-ci-demo:1.0.0 .'
            }
        }
        stage('Push Docker Image'){
            steps{
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]){
                    bat '''
                        docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                        docker push ctnsrma/docker-ci-demo:1.0.0
                    '''
                }
            }
        }
    }
}