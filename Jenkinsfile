pipeline {
    agent any
    tools {dockerTool  "myDocker" } 
    environment {
        p = sh(script: 'echo $PATH', returnStdout: true).trim()
        PATH = "/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    }

    stages {
        stage ('Initialize') {
            steps {
                    script {
            def dockerHome = tool 'myDocker'
            env.PATH = "${dockerHome}/bin:${env.PATH}"
            sh(script: 'echo $PATH', returnStdout: true).trim()
            sh(script: "echo ${dockerHome}", returnStdout: true).trim()
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
