pipeline {
    agent any

    environment {
        ECR_REGISTRY_ID = '352708296901.dkr.ecr.us-west-1.amazonaws.com'
    }

    stages {
        stage('Build and Push') {
            steps {
                script {
                    sh "aws ecr get-login-password --region us-west-1 | docker login --username AWS --password-stdin $ECR_REGISTRY_ID"
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

        stage('Trigger Deploy') {
            steps {
                build job: 'RobertaDeploy' , wait: false, parameters: [
                    string(name: 'Roberta_IMAGE_URL', value: "${ECR_REGISTRY_ID}/jenkins:0.0.${BUILD_NUMBER}")
                ]
            }
        }
    }
}