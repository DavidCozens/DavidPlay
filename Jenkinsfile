pipeline{
  agent {
    docker {
      image 'gcc:12.2.0'
      registryCredentialsId 'dockerhub'
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'gcc -o DavidPlay DavidPlay.c'
      }
    }
    stage('Run') {
      steps {
        sh label: 'Run DavidPlay', script: './DavidPlay'
      }
    }
  }
}
