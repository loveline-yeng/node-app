pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker image'){
            steps{
                sh "docker build . -t yengwia/nodeapp:${DOCKER_TAG}"
            }
        }
        stage('DockerHub Push'){
                steps{
                    withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerHubPwd')]) {
                    sh "docker login -u yengwia -p ${dockerHubPwd}"
                    sh "docker push yengwia/nodeapp:${DOCKER_TAG}"
                }
            }

        }
    }
}

def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}