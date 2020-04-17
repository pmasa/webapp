pipeline {
 environment {
    registry = "pedromasa/webapp"
    registryCredential = 'dockerhub'
    dockerImage = ''
 }
 agent any
 stages {
    stage('Env variables') {
        steps {
            sh "printenv"
        }
    }
    stage('Cloning Git') {
        steps {
            git 'ssh://git@192.168.0.114:2222/git-server/repos/webapp.git'
        }
    }
    stage('Building Docker Image') {
        steps{
            script {
                dockerImage = docker.build("pedromasa/webapp:${env.BUILD_ID}", "-f project/webapp/Dockerfile .")
            }
        }
    }
    stage('Push Image to Docker Hub ') {
        steps{
            script {
                docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                    dockerImage.push('latest')
                }
            }
        }
    }
 }

}
