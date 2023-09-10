pipeline{
    agent any
    stages{
         stage("Deploy") {
            steps {
                script {
                    withAWS(credentials: 'AWS-Credentials') {
                       sh 'aws ec2 describe-instances --region us-east-2'
                    
                    withKubeConfig(clusterName: 'EKS-DEV', contextName: 'arn:aws:eks:us-east-2:855326247041:cluster/EKS-DEV', credentialsId: 'kubeconfigfile', namespace: 'default', serverUrl: 'https://CD4331F2B06F91536EEE778E45EBB862.gr7.us-east-2.eks.amazonaws.com') {
                         sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'  
                         sh 'chmod u+x ./kubectl' 
                        sh 'aws eks update-kubeconfig --name EKS-DEV --region us-east-2'
                         sh './kubectl get nodes'
                    }
                 }
                }
            }
        }
}
}
