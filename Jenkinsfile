pipeline {
    agent any

    stages {
        stage ('Build Image') {
            steps {
                script{
                    dockerapp = docker.build("matheus-mprado/api-produto", '-f ./src/Dockerfile ./src')
                }
            }
        }

    }
}