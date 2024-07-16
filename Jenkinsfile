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

        stage('Stop and Remove Existing Container') {
            steps {
                script {
                    // Varolan container'ı durdur ve sil
                    bat """
                    docker stop demo-container
                    IF %ERRORLEVEL% NEQ 0 (
                        echo Container durdurulamadı veya zaten yok
                    )
                    docker rm demo-container
                    IF %ERRORLEVEL% NEQ 0 (
                        echo Container silinemedi veya zaten yok
                    )
                    """
                }
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
                    docker.image("demo/app:${env.BUILD_NUMBER}").run("-d -p 1010:1515 --name demo-container")
                }
            }
        }
    }
}