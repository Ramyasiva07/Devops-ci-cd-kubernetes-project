pipeline {
    agent any   

    environment {
        IMAGE_NAME = "ramyasiva07/portfolio"
    }

    stages {

        stage('Build Image') {
            steps {
                bat 'docker build --no-cache -t %IMAGE_NAME%:v2 .'
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                    bat 'docker push %IMAGE_NAME%:v2'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s/ --validate=false'
                bat 'kubectl rollout restart deployment portfolio'
            }
        }
    }
}
