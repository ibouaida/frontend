pipeline {
    agent {label 'devops'}

    environment {
        DOCKER_PASSWORD=credentials('DOCKER_PASSWORD')
    }

    stages {
        stage('Docker login') {
            steps {
                script {
                    sh 'echo $DOCKER_PASSWORD | docker login -u ibou1984 --password-stdin'
                }
            }
        }

        stage('Docker build image') {
            steps {
                script {
                    sh 'docker build -t frontend:v1.1.0 .'
                }
            }
        }

        stage('Docker tag image') {
            steps {
                script {
                    sh 'docker tag frontend:v1.1.0 ibou1984/frontend:v1.1.0'
                }
            }
        }

        stage('Docker push image') {
            steps {
                script {
                    sh 'docker push ibou1984/frontend:v1.1.0'
                }
            }
        }
          stage('Deploy to kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f manifests'
                }
            }
        }
    }
}
