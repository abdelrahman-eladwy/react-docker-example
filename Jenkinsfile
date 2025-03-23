pipeline {
    agent any  

    environment {
        DOCKER_HUB_CREDS = credentials('docker-hub-credentials')
        DOCKER_IMAGE_NAME = "eladwy/react-app"
        DOCKER_IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image from the Dockerfile
                    sh """
                        docker build -t ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} .
                    """
                }
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', 
                    passwordVariable: 'dockerHubPassword', 
                    usernameVariable: 'dockerHubUser')]) {
                    // Login to Docker Hub and push the image
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}"
                }
            }
        }

        stage('Deploy Docker Container') {
            steps {
                script {
                    // Run the Docker container from the pushed image
                    sh """
                        docker stop my-app || true && docker rm my-app || true
                        docker run -d --name my-app -p 80:80 ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image built, pushed, and deployed successfully!'
            
            mail to: 'abdoahmed32522@gmail.com',
                 subject: "SUCCESS: Jenkins Job '${env.JOB_NAME}' (#${env.BUILD_NUMBER})",
                 body: "The build succeeded! Check Jenkins for details: ${env.BUILD_URL}"
        }
        failure {
            echo 'Build or deployment failed!'
            
            mail to: 'abdoahmed32522@gmail.com',
                 subject: "FAILURE: Jenkins Job '${env.JOB_NAME}' (#${env.BUILD_NUMBER})",
                 body: "The build failed! Check Jenkins for details: ${env.BUILD_URL}"
        }
    }
}