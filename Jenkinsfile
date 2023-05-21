pipeline{
    agent any

    stages {
        stage ('Build Image'){
            steps {
                script {
                    dockerapp = docker.build("matheusmprado/api-produto","-f ./src/Dockerfile ./src")
                }
            }
        }
    }
}