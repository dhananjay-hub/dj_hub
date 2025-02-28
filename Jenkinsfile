pipeline {
    agent any

    environment {
        DOCKER_CREDS = credentials('dockerhub-credentials') // Use Docker credentials stored in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm // Ensures the latest code from the repository is pulled.
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    // Inject Docker Hub credentials and use them to log in
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', 
                                                       usernameVariable: 'DOCKER_USERNAME', 
                                                       passwordVariable: 'DOCKER_PASSWORD')]) {
                        // Login to Docker Hub
                        sh '''
                            echo "Logging into Docker Hub..."
                            docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                        '''
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build the Docker image (replace with your own Docker image name/tag)
                    echo "Building Docker image..."
                    sh '''
                        docker build -t my-app .
                    '''
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline completed"
        }
        success {
            echo "Build completed successfully"
        }
        failure {
            echo "Build failed"
        }
    }
}
