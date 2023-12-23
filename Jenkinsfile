pipeline {
    agent {label 'Node_Docker'}
    stages {
        stage('vcs') {
            steps {
                git branch: 'dev-container', 
                    url: 'https://github.com/dummyreposito/nopCommerceJuly23.git'    
            }
            
        }
        stage('package') {
            steps {
                sh 'docker image build -t nopcommerce:latest .'
                sh 'docker image tag nopcommerce:latest ajaykumarramesh/nopcommerce:latest'
                sh 'docker image push ajaykumarramesh/nopcommerce:latest'
                
            }            
        }
        stage('terraform') {
            steps {
                sh 'cd deploy_Infrastructure && terraform init && terraform apply -auto-approve' 
                //sh 'echo "$(terraform output kube_config)" > ./azurek8s && export KUBECONFIG=./azurek8s && kubectl apply -f ../k8s/nop-deploy.yaml'
            }
        }
        stage('k8s_deploy'){
            steps{
            sh 'az aks get-credentials --resource-group rg-mutual-hare --name cluster-logical-heron && kubectl apply -f ./k8s/nop-deploy.yaml' 
            }

        }

    }
}

