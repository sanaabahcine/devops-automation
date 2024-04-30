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
                    app = docker.build("sanaeabahcine371/devops-integration .")
            
                }
            }
        }
        stage('push mage to dockerhub'){
               docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
               }

              }
             
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}




    }
}
