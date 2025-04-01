pipeline {
    agent any
    environment {
        CLUSTER_NAME = 'sample-devops-cluster'
        AWS_REGION = 'us-east-2'
        DEPLOYMENT_NAME = 'java-app'
        IMAGE_NAME = 'sampledevops'
    }
    stages {
        stage('Checkout Code') {
           steps {
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/Areeza-git/sample-devops.git']]
                ])
            }
        }
        stage('Build and Package') {
            steps {
                sh 'mvn clean package'  
            }
        }
        stage('Build and Push Docker Image') {
            steps {
                sh '''
                    docker build -t $IMAGE_NAME .
                    docker tag $IMAGE_NAME:latest 438979369835.dkr.ecr.us-east-2.amazonaws.com/sample-devops:latest
                    docker push 438979369835.dkr.ecr.us-east-2.amazonaws.com/sample-devops:latest
                '''
            }
        }
        stage('Deploy to EKS') {
            steps {
                sh '''
                    aws eks update-kubeconfig --region $AWS_REGION --name $CLUSTER_NAME
                    kubectl apply -f k8s/deploy.yaml
                '''
            }
        }
    }
}
