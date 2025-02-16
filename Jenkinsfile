pipeline {
    agent any
    
    tools{
        maven "Maven-3.9.9"
    }    

    stages {
        stage('Git Clone') {
            steps {
               git branch: 'main', url: 'https://github.com/vinodses/01_products_api.git'
            }
        }
        stage('Maven Build'){
            steps{
             sh 'mvn clean package'
            }
        }
        stage('Docker Image'){
            steps{
             sh 'docker build -t vinodses/products_api .'
            }
        }
        stage('Docker Image push'){
            steps
            withCredentials([string(credentialsId: 'docker_pwd', variable: 'docker_pwd')]) {
                   sh 'docker login -u vinodses -p ${docker_pwd}'
                   sh 'docker push vinodses/products_api'
            }
            }
        }
        stage('k8s deployment'){
            steps{
             sh 'kubectl apply -f Deployment.yml'
            }
        }        
    }
}
