pipeline{
    agent any
    tools{
        maven 'MAVEN_HOME'
    } 
    environment{
        dockerImage = ''
        registry = 'izhaan2021/docker-jenkins-integration-sample'
        registryCredential = 'dockerhub_id'
    }
    
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/GhufranAhmad992/docker-jenkins-integration-sample']])
                bat 'mvn clean install'
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    dockerImage = docker.build registry
                }
            }
        }
        
        stage('Upload Image On DockerHub'){
            steps{
                script{
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                    
                }
            }
        }
        
        
    }
    
}