pipeline {
    agent{label 'prod'}
    stages{
        stage('Checkout'){
            steps{
            git branch: 'main', url: 'https://github.com/chia5/nodejs_k8s_deploy.git'
            }
        }
        
        stage('Package'){
            steps{
            echo "Stared Build Stage"
            }
        }
        
        stage("Test"){
            steps{
            echo "Strated Testing"
            }
            
        }
        
        stage("Build Image"){
            steps{
                script{
                    dockerImage = docker.build ('chash07/nodeapp')
                }
            }
        }
        
        stage('Push Image'){
            steps{
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                        dockerImage.push("latest")
                    }
                }
            }
        }
        
        stage('Deploying to K8s'){
            steps{
                script{
                    kubernetesDeploy(configs:'deploymentservice.yml', kubeconfigId:'Kubernetes_Cluster_Config')
                }
            }
        }
        
        
    }
}
