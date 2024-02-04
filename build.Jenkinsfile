pipeline {
    agent any

    environment {
        ECR_REGISTRY_ID = 'public.ecr.aws/r7m7o9d4'
        IMAGE_NAME = ''
        DOCKERFILE_PATH = 'Dockerfile'
        AWS_CREDENTIALS_ID = 'AWS_CREDENTIALS_ID'
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Get AWS credentials from Jenkins credentials
                    withCredentials([usernamePassword(credentialsId: AWS_CREDENTIALS_ID, passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {

                        // Authenticate Docker with ECR
                        sh "aws ecr-public get-login-password --region $AWS_DEFAULT_REGION | docker login --username AWS --password-stdin $ECR_REGISTRY_ID"

                        // Build and push Docker image
                        sh "docker build -t $IMAGE_NAME -f $DOCKERFILE_PATH ."
                        sh "docker tag $IMAGE_NAME:latest $ECR_REGISTRY_ID/$IMAGE_NAME:latest"
                        sh "docker push $ECR_REGISTRY_ID/$IMAGE_NAME:latest"
                    }
                }
            }
        }
    }
}
