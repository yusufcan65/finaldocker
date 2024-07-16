pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // GitHub'dan kodları checkout et
                checkout scmGit(
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/yusufcan65/finaldocker.git']]
                )
            }
        }

        

        stage('Build Docker Image') {
            steps {
                script {
                    // Docker image'ını oluştur
                    docker.build("demo/app:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Docker container'ı çalıştır
                    docker.image("demo/app:${env.BUILD_NUMBER}").run("-d -p 1515:8080 --name demo-container")
                }
            }
        }
    }
}