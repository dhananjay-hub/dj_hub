pipeline {
    agent any

    environment {
        DOCKER_CREDS = credentials('dockerhub-credentials')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo "Building Docker image..."
                    // Example build step
                    sh 'docker build -t my-app .'
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline completed"
        }
    }
}
