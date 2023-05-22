pipeline {
    agent any

    environment {
        DOCKER_HOME = tool 'myDocker'
        PATH = "${DOCKER_HOME}/bin:${env.PATH}"
        DOCKER_IMAGE_TAG = "v${env.BUILD_ID}"
    }

    stages {
        stage('Initialize') {
            steps {
                script {
                    def dockerapp
                    dockerapp = docker.build("matheusmprado/api-produto:${DOCKER_IMAGE_TAG}", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage('Build Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${DOCKER_IMAGE_TAG}")
                    }
                }
            }
        }
    }
}