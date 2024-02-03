pipeline {
    agent any

    environment {
        ECR_REGISTRY_ID = 'public.ecr.aws/r7m7o9d4/jihad'
        IMAGE_NAME = 'jihadroberta-image'
        DOCKERFILE_PATH = 'Dockerfile'
        AWS_DEFAULT_REGION = 'us-west-1'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Build and push Docker image
                    sh "docker build -t $IMAGE_NAME -f $DOCKERFILE_PATH ."
                    sh "docker tag $IMAGE_NAME:latest $ECR_REGISTRY_ID/$IMAGE_NAME:latest"
                    sh "docker push $ECR_REGISTRY_ID/$IMAGE_NAME:latest"
                }
            }
        }
    }
}