pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')
        AWS_DEFAULT_REGION    = 'us-east-1'
    }
    parameters {
        booleanParam(name:"TF_INIT", defaultValue:true, description:"Run Terraform Init")
        booleanParam(name:"TF_VALIDATE", defaultValue:true, description:"Run Terraform Validate")
        booleanParam(name:"TF_PLAN", defaultValue:true, description:"Run Terraform Plan")
        booleanParam(name:"TF_APPLY", defaultValue:false, description:"Run Terraform Apply")
        booleanParam(name:"TF_DESTROY", defaultValue:false, description:"Run Terraform Destroy")
    }

    stages {
        stage('Test AWS Credentials') {
    steps {
        sh 'aws sts get-caller-identity'
    }
}
        stage('Terraform Init') {
            when {
                expression { params.TF_INIT }
            }
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Validate') {
            when {
                expression { params.TF_VALIDATE }
            }
            steps {
                sh 'terraform validate'
            }
        }

        stage('Terraform Plan') {
            when {
                expression { params.TF_PLAN }
            }
            steps {
                sh 'terraform plan'
            }
        }

        stage('Terraform Apply') {
            when {
                expression { params.TF_APPLY }
            }
            steps {
                sh 'terraform apply -auto-approve'
            }
        }
        
        stage('Terraform Destroy') {
            when {
                expression { params.TF_DESTROY }
            }
            steps {
                sh 'terraform destroy -auto-approve'
            }
        }
    
    }
}
