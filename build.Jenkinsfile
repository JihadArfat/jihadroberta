pipeline {
    agent any

    environment {
        ECR_REGISTRY_ID = 'public.ecr.aws/r7m7o9d4/jihad'
        IMAGE_NAME = 'jihadroberta-image'
        DOCKERFILE_PATH = 'Dockerfile'
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage('Build and Push') {
            steps {
                script {
                    // Authenticate Docker with ECR
                    sh "aws ecr-public get-login-password --region $AWS_DEFAULT_REGION | docker login --username AWS --password-stdin $ECR_REGISTRY_ID"

                    // Build, tag, and push Docker image
                    sh "docker build -t $IMAGE_NAME -f $DOCKERFILE_PATH ."
                    sh "docker tag $IMAGE_NAME:latest $ECR_REGISTRY_ID:latest"
                    sh "docker push $ECR_REGISTRY_ID:latest"
                }
            }
        }
    }
}
