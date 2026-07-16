pipeline {
    agent any

    environment {
        DOCKER_CREDS_ID = 'docker-credentials' 
        GIT_CREDS_ID    = 'github-credentials'
        IMAGE_NAME = 'ieliyahu1971/final-app'
        IMAGE_TAG  = "v${env.BUILD_NUMBER}"
        GIT_REPO_URL = 'https://github.com/eliyahui1971-il/finaldev.git'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: DOCKER_CREDS_ID, passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                        sh "echo \$DOCKER_PASS | docker login -u \$DOCKER_USER --password-stdin"
                        sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                    }
                }
            }
        }

        stage('Update Helm Values & Push to Git') {
            steps {
                script {
                    sh """
                    sed -i 's/tag: ".*"/tag: "${IMAGE_TAG}"/' helm/values.yaml
                    """
                    
                    sh """
                    git config user.email "jenkins@your-domain.com"
                    git config user.name "Jenkins CI"
                    """
                    
                    withCredentials([usernamePassword(credentialsId: GIT_CREDS_ID, passwordVariable: 'GIT_PASS', usernameVariable: 'GIT_USER')]) {
                        sh """
                        git add helm/values.yaml
                        git commit -m "Update image tag to ${IMAGE_TAG} [skip ci]"
                        git push https://${GIT_USER}:${GIT_PASS}@github.com/eliyahui1971-il/finaldev.git HEAD:main
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed."
        }
    }
}