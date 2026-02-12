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
node { // <--- Esto es lo que te falta, le asigna un espacio de trabajo
    stage('Deploy to EKS') {
        withCredentials([
            string(credentialsId: 'aws-access-key-id', variable: 'AWS_ACCESS_KEY_ID'),
            string(credentialsId: 'aws-secret-access-key', variable: 'AWS_SECRET_ACCESS_KEY'),
            string(credentialsId: 'aws-session-token', variable: 'AWS_SESSION_TOKEN')
        ]) {
            // Ahora 'sh' sí sabe dónde ejecutarse
            sh "aws eks update-kubeconfig --name TU_CLUSTER_NAME --region us-east-1"
            sh "kubectl get pods"
            sh 'cat /etc/os-release' // Te dirá qué Linux es
            sh 'whoami'             // Te dirá qué usuario está usando Jenkins
            sh 'aws --version'      // Verificará si tienes la herramienta instalada
        }
    }
}
```

