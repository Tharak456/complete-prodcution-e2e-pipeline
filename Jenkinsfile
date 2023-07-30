pipeline{
    agent any
    tools {
        jdk 'Java17'
        maven 'Maven3'
          }
    environment {
        RELEASE = "1.0.0"
        DOCKER_USER = '2356176'
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "test"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
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
                    withDockerRegistry(credentialsId: 'DOCKER_PASS') {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }
                    withDockerRegistry(credentialsId: 'DOCKER_PASS') {
                        docker_image.push("${IMAGE_TAG}")
                    }
            }

        }

        
        
    }
        stage("Deploy") {
            steps {
                script {
                    withAWS(credentials: 'AWS-Credentials') {
                       sh 'aws ec2 describe-instances'
                    
                    withKubeConfig(clusterName: 'EKS-DEV', contextName: 'arn:aws:eks:us-east-2:114100840324:cluster/EKS-DEV', credentialsId: 'k8sconfig', namespace: 'default', restrictKubeConfigAccess: false, serverUrl: 'https://68D32B1E466F6F6EEC3F734DE5152A90.sk1.us-east-2.eks.amazonaws.com') {
                         sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'  
                         sh 'chmod u+x ./kubectl'  
                         sh './kubectl get nodes'
                    }
                 }
                }
            }
        }
}
}
