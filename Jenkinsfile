pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1' // Change this if needed
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/jananikirubakaran/terraform-aws-jenkins.git'
            }
        }

        stage('Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Validate') {
            steps {
                sh 'terraform validate'
            }
        }

        stage('Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Apply') {
            steps {
                input "Do you want to apply the changes?"
                sh 'terraform apply tfplan'
            }
        }
    }
}

