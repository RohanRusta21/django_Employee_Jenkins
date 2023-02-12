pipeline {
    agent any
    environment {
        registery = "public.ecr.aws/w1u8s8d4/django_employee"
    }

    stages {
        stage('Github Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/new']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/RohanRusta21/django_Employee_Jenkins.git']])
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    customImage = docker.build registery+":$BUILD_ID"
                }
            }
        }
        stage('Push Into ECR'){
            steps{
                script{
                    sh 'aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/w1u8s8d4'
                    customImage.push()
                }
            }
        }
    }
}
