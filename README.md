# Jenkins - Ubuntu - EKS

## Install Jenkins and EKS
```
https://www.digitalocean.com/community/tutorials/how-to-install-jenkins-on-ubuntu-22-04
```
```
https://aws.plainenglish.io/building-an-end-to-end-ci-cd-pipeline-with-jenkins-and-amazon-eks-a-step-by-step-guide-8e4d659d9a54
```

## Jenkins Pipeline 
```
Use Secret Text in Management-Credentials, no "aws credentials".
```
```
pipeline {
    agent any 
    
    stages {
        stage('EKS Check') {
            steps {
                withCredentials([
                    string(credentialsId: 'aws-access-key-id', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'aws-secret-access-key', variable: 'AWS_SECRET_ACCESS_KEY'),
                    string(credentialsId: 'aws-session-token', variable: 'AWS_SESSION_TOKEN')
                ]) {
                    sh "aws eks update-kubeconfig --name demo-cluster --region us-east-1"
                    sh "kubectl get nodes"
                    sh 'cat /etc/os-release' 
                    sh 'whoami'             
                    sh 'aws --version'  
                }
            }
        }
    }
}
```





