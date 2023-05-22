pipeline {
    agent any
    // tools {dockerTool  "myDocker" } 
    stages {
        stage ('Initialize') {
            steps {
                script {
                     // Configuração do ambiente Docker
                    def dockerHome = tool name: 'myDocker', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
                    env.PATH = "${dockerHome}/bin:${env.PATH}"
                }
            }
        }

        stage ('Build Image') {
            steps {
                script {
                    dockerapp = docker.build("matheusmprado/api-produto:v${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage ('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
    }
}
