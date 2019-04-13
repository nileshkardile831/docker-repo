pipeline {
  environment {
    registry = "nileshkardile831/nkardile-cybage"
    registryCredential = 'nileshkardile831'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
	git 'https://github.com/nileshkardile831/docker-repo.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
