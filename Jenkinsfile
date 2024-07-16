pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/yusufcan65/jenkins-github-docker-connect.git']]
                )
                 bat 'mvn clean install'
            }
        }

          stage('Stop and Remove Existing Container') {
                                               steps {
                                                   script {
                                                    // Varolan container'ı durdur ve sil
                                                            bat 'docker stop demo-container '
                                                            bat 'docker rm demo-container'
                                                         }
                                                    }
                                         }


        stage('Build docker image'){
            steps{
                script{
                    docker.build("yusuf65:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                    docker.image("yusuf65:${env.BUILD_NUMBER}").run("-d -p 6534:5050 --name demo-container")
                }
            }
  }
}

}