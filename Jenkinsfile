pipeline{
  agent {
    docker {
      image 'gcc:12.2.0'
      registryCredentialsId 'dockerhub'
    }
  }
  stages {
    stage('echo') {
      steps {
        echo 'Hello World'
      }
    }
  }
}
