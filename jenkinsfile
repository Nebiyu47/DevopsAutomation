pipeline {
    agent any
    tools{
        maven 'mave_3.8.6'
    }
    stages{
        stage('Build maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Nebiyu47/DevopsAutomation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image'){
            steps{
                sh 'docker build -t neba56/devops-integration .'
            }
        }
        stage('Push to Docker Hub'){
            steps{
                withCredentials([string(credentialsId: 'dockerHub', variable: 'dockerHub')]) {
                sh 'docker login -u neba56 -p ${dockerHub}'
        }
                sh 'docker push neba56/devops-integration'
            }
        }
    }
}