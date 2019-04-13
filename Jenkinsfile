pipeline {
  environment {
    registry = "nileshkardile831/nkardile-cybage"
    registryCredential = 'docker-hub-credentials'
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
	  stage('Pull image and start a container'){
		  steps{
			  sh "docker pull $registry:$BUILD_NUMBER"
			  sh "docker run -td -p 80:80 $registry:$BUILD_NUMBER /bin/bash"
		  }
	  }
  }
}
