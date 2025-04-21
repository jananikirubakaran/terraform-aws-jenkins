pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        TF_VAR_environment = 'dev'
    }

    options {
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/jananikirubakaran/terraform-aws-jenkins.git', branch: 'main'
            }
        }

        stage('Terraform Init') {
            steps {
                withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                    sh 'terraform init'
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                    sh 'terraform plan'
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                input message: 'Do you want to apply the changes?'
                withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                    sh 'terraform apply -auto-approve'
                }
            }
        }
    }
}

