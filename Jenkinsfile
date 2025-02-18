pipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-1'
    }
    stages {
        stage('Init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }
        stage('Approval') {
            when {
                branch 'prod'
            }
            steps {
                input message: "Approve deployment to production?"
            }
        }
        stage('Apply') {
            steps {
                sh 'terraform apply -auto-approve'
            }
        }
    }
}
