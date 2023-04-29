pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/amisha-2500/devops-automation.git']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t amisha124/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
                   sh 'docker login -u amisha124 -p ${dockerhub}'

}
                   sh 'docker push amisha124/devops-integration'
                }
            }
        }
       stage('Deploy') {
           steps{
               sh 'docker run -d -p 8081:8080 amisha124/devops-integration'
}
       }
    }
}
