pipeline {
    agent any

    environment {
        ECR_REGISTRY_ID = '352708296901.dkr.ecr.us-west-1.amazonaws.com'
        AWS_DEFAULT_REGION = 'us-west-1'
    }

    stages {
        stage('Build and Push') {
            steps {
                script {
                    sh "aws ecr-public get-login-password --region $AWS_DEFAULT_REGION | docker login --username AWS --password-stdin $ECR_REGISTRY_ID"
                    sh "docker build -t $ECR_REGISTRY_ID/jenkins:0.0.$BUILD_NUMBER ."
                    sh "docker push $ECR_REGISTRY_ID/jenkins:0.0.$BUILD_NUMBER"
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
