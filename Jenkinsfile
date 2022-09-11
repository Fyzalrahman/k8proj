pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Fyzalrahman/k8proj.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t k8image /var/lib/jenkins/workspace/kubepro'
                sh 'sudo docker tag k8image fyzalrahman/k8image:latest'
                sh 'sudo docker tag k8image fyzalrahman/k8image:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push fyzalrahman/k8image:latest'
                sh 'sudo docker image push fyzalrahman/k8image:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'kubectl apply -f /var/lib/jenkins/workspace/kubepro/k8DeployPod.yaml'
                sh 'kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
