pipeline{
    agent any
    tools {
        jdk 'Java17'
        maven 'Maven3'
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

        
    }
}

