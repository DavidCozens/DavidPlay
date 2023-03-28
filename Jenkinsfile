pipeline{
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'gcc:12.2.0'
          registryCredentialsId 'dockerhub'
        }
      }
      options {
        skipDefaultCheckout true
      }
      steps {
        checkout scm
        sh 'gcc -o DavidPlay DavidPlay.c'
      }
    }
    stage('Run') {
      agent {
        docker {
          image 'gcc:12.2.0'
          reuseNode true
          registryCredentialsId 'dockerhub'
        }
      }
      options {
        skipDefaultCheckout true
      }
      steps {
        sh label: 'Run DavidPlay', script: './DavidPlay'
      }
    }
    stage('Publish') {
      agent {
        docker {
          image 'gcc:12.2.0'
          reuseNode true
          registryCredentialsId 'dockerhub'
        }
      }
      options {
        skipDefaultCheckout true
      }
      steps {
        archiveArtifacts artifacts: 'DavidPlay', followSymlinks: false
        fingerprint 'DavidPlay'
      }
    }
    stage('Cleanup') {
      agent {
        docker {
          image 'gcc:12.2.0'
          reuseNode true
          registryCredentialsId 'dockerhub'
        }
      }
      options {
        skipDefaultCheckout true
      }
      steps {
        cleanWs()
      }
    }
  }
}
