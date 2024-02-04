pipeline {
    agent any

    parameters {string(name: 'Roberta_IMAGE_URL', defaultValue: '', description: '') }

    stages {
        stage('Deploy') {
            steps {
                // complete this code to deploy to real k8s cluster
                sh 'echo $Roberta_IMAGE_URL'
                sh '# kubectl apply -f ....'
            }
        }
    }
}
