pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // GitHub'dan kodları checkout et
                git branch: 'main', url: 'https://github.com/yusufcan65/finaldocker.git'
            }
        }

        stage('Stop and Remove Existing Container') {
            steps {
                script {
                    // Varolan container'ı durdur ve sil
                    bat 'docker stop demo-container || exit 0'
                    bat 'docker rm demo-container || exit 0'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Docker image'ını oluştur
                    bat 'docker build -t demo/app:%BUILD_NUMBER% BUILD/web'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Docker container'ı çalıştır
                    bat 'docker run -d -p 1515:8080 --name demo-container demo/app:%BUILD_NUMBER%'
                }
            }
        }
    }
}