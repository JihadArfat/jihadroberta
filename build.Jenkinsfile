pipeline {
    agent any

    environment {
        ECR_REGISTRY_ID = 'public.ecr.aws/r7m7o9d4/jihad'
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage('Build and Push') {
            steps {
                script {
                    sh "aws ecr-public get-login-password --region $AWS_DEFAULT_REGION | docker login --username AWS --password-stdin $ECR_REGISTRY_ID"
                    sh "docker build -t $ECR_REGISTRY_ID/jihadroberta:0.0.$BUILD_NUMBER ."
                    sh "docker push $ECR_REGISTRY_ID/jihadroberta:0.0.$BUILD_NUMBER"
                }
            }
            post {
                always {
                    sh 'docker image prune -a --force'
                }
            }
        }
    }
}
