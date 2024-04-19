pipeline {
    agent any

    stages {
        stage('Approval to Deploy') {
            steps {
                input 'Approve to Deploy in k8s'
            }
        }
        
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8s', namespace: 'webapps', serverUrl: 'https://C1B4E725E90821EBC45F5F89AE6AE746.sk1.us-east-1.eks.amazonaws.com']]) {
                    sh 'kubectl apply -f deployment-service.yml'
                    sleep 60
                    // Replace 'deployment.yaml' with the path to your Kubernetes deployment YAML file
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8s', namespace: 'webapps', serverUrl: 'https://C1B4E725E90821EBC45F5F89AE6AE746.sk1.us-east-1.eks.amazonaws.com']]) {
                    sh 'kubectl get pods,services,deployments -n webapps'
                    // Or any other verification commands you want to run
                }
            }
        }
    }
}
