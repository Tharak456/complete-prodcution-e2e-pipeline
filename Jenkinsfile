pipeline{
    agent any
   
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

        }
}

