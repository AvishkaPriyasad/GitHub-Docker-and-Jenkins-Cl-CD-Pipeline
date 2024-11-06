pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/AvishkaPriyasad/GitHub-Docker-and-Jenkins-Cl-CD-Pipeline.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t avishkapriyasad/nodeapp-test:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'test-dockerpassword', variable: 'test-dockerhubpass')]) {
                    
                        bat "docker login -u avishkapriyasad -p %test-dockerhubpass%"
                    
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push avishkapriyasad/nodeapp-test:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
