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
    stage('') {
  parallel {
    // One or more stages need to be included within the parallel block.

    stage('Ubuntu') {
      agent {
        docker {
          image 'ubuntu:lunar'
          reuseNode true
          registryCredentialsId 'dockerhub'
        }
      }
      options {
        skipDefaultCheckout true
      }
      steps {
        sleep 5
        sh label: 'Run DavidPlay', script: './DavidPlay'
      }
    }
        stage('debian') {
      agent {
        docker {
          image 'debian:bookworm'
          reuseNode true
          registryCredentialsId 'dockerhub'
        }
      }
      options {
        skipDefaultCheckout true
      }
      steps {
        sleep 10
        sh label: 'Run DavidPlay', script: './DavidPlay'
      }
    }
      }
  }
    stage('Publish') {
      agent {
        docker {
          image 'ubuntu:lunar'
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
          image 'ubuntu:lunar'
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
