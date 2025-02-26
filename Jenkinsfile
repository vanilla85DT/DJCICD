pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo "Checkout"
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        credentialsId: 'supervanilla85',
                        url: 'https://github.com/vanilla85DT/DJCICD.git'
                    ]]
                ])
                echo "Checkout done"
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh '/usr/local/bin/docker pull --disable-content-trust=false node:20-alpine'
                    sh '/usr/local/bin/docker build -t csi402-app-image .'

                    sh '/usr/local/bin/docker run -d --name csi-container -p 54100:3000 csi402-app-image:latest'
                }
            }
        }
    }
}
