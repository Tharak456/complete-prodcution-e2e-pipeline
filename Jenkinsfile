pipeline{
    agent any
    tools {
        jdk 'Java17'
        maven 'Maven3'
          }
    environment {
        DOCKER_USER = "2356176"
        DOCKER_PASS = 'dockerhub'
    }
    stages{
        stage("Cleanup Workspace"){
            steps {
                cleanWs()
                  }

                                  }
    
        stage("Checkout from SCM"){
            steps {
                git branch: 'CICD', credentialsId: 'GITHUB', url: 'https://github.com/Tharak456/complete-prodcution-e2e-pipeline.git'
                  }

                                  }

        stage("Build Application"){
            steps {
                sh "mvn clean package"
                  }

                                  }

        stage("Test Application"){
            steps {
                sh "mvn test"
                  }

                                  }
        stage("code analysis using sonarqube"){
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'Sonarqube-Token') {
                        sh "mvn sonar:sonar"
                  }
                       }
                           } 
        }
                stage("Build & Push Docker Image") {
            steps {
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }
                }
            }

        }

        
        
    }
}

