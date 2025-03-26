pipeline {
    agent any
    environment {
        IMAGE_NAME = 'sampledevops'
        REGISTRY = '3.128.79.118:5000'
    }
    stages {
        stage('Compile') {
            steps {
                build job: 'Compile_Job'
            }
        }
        stage('Test') {
            steps {
                build job: 'Test_Job'
            }
        }
        stage('Package') {
            steps {
                build job: 'Package_Job'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $REGISTRY/$IMAGE_NAME:latest .'
            }
        }
        stage('Push Docker Image') {
            steps {
                sh 'docker push $REGISTRY/$IMAGE_NAME:latest'
            }
        }
    }
}
