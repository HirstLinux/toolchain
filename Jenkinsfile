def image
pipeline {
  agent any
  stages {
    stage('Build Docker Image') {
      steps {
        script {
          dir('container-build') {
              image = docker.build("toolchain:${env.BUILD_ID}")
          }
        }
      }
    }
    stage('Build Toolchain Stage 1') {
      steps {
        script {
          image.inside {
            sh "cd /home/docker/scripts"
            sh "01-toolchain-pass1"
          }
        }
      }
    }
    stage('Build Toolchain Stage 2') {
      steps {
        script {
          image.inside {
            sh "cd /home/docker/scripts"
            sh "01-toolchain-pass2"
          }
        }
      }
    }
    stage('Collect Build Artifacts') {
      steps {
        script {
          image.inside('-v $WORKSPACE:/target -u root') {
            sh "cd /output;tar -czvf /target/toolchain-${env.BUILD_ID}.tar.gz lfs"
          }
        }
      }
    }
  }
  post {
    always {
      archiveArtifacts "$WORKSPACE/*.tar.gz"
    }
  }
}