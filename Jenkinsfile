pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    environment {
        registry = "impothini/nodeapp"
        registryCredential = 'reg-cred'
  }
    stages {
        stage('scm checkout') {
            steps {
                script{
                    gitVar= git ( branch: 'master', url: 'https://github.com/impothini/NodeApp.git')
                }
            }
        }
        stage('Docker Build') {
            steps {
                script{
                    dockerImage = docker.build registry 
                }
            }
        }
        stage('Push Image') {
          steps{
            script {
                docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
                dockerImage.push("${gitVar.GIT_LOCAL_BRANCH}-${env.BUILD_NUMBER}")
                dockerImage.push("latest")
              }
            }
          }
        }
    }
}

