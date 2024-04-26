pipeline {
    agent any
    tools {
        maven 'maven_3_5_0'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sanaabahcine/devops-automation']])
                sh'mvn clean install'
            }

        }
        stage('Build docker image') {
            steps {
                script {
                    sh 'docker build -t sanaeabahcine371/devops-integration .'
                }
            }
        }
        stage('push mage to dockerhub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u sanaeabahcine371 -p ${dockerhubpwd}'


              }
              sh 'docker push sanaeabahcine371/devops-integration'
                }
            }
        }





    }
}
