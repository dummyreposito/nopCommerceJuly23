pipeline {
    agent any
    stages {
        stage('vcs') {
            steps {
                git branch: 'devc', 
                    url: 'https://github.com/CICDProjects/nopCommerceJuly23.git'    
            }
            
        }
        stage('package') {
            steps {
                sh 'docker image build -t nopcommerce:latest .'
                sh 'docker image tag nopcommerce:latest shaikkhajaibrahim/nopcommerceaug23:latest'
                sh 'docker image push shaikkhajaibrahim/nopcommerceaug23:latest'
                
            }            
        }
    }
}