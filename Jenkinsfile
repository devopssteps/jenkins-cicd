pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/devopssteps/jenkins-cicd']])
                sh 'mvn clean install'
            }
        }
        stage('build docker image'){
            steps{
                sh 'docker build -t rajivsiddiqui/devops-integration .'
            }
        }
        stage('push image to dockerhub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u rajivsiddiqui -p ${dockerhubpwd}'
                    }
                    
                    sh 'docker push rajivsiddiqui/devops-integration'
                }
            }
            
        }
    }
        
}