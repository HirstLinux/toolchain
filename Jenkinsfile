pipeline {
  agent any
  stages {
    stage('Build Docker Image') {
      steps {
        script {
          dir('container-build') {
            def image = docker.build("toolchain:${env.BUILD_ID}")
          }
        }
      }
    }
    stage('Build Toolchain Stage 1') {
      steps {
        scripts {
          dir('container-build') {
            image.inside('-v $WORKSPACE:/target -u root') {
              sh "cd /home/docker/scripts"
              bash "01-toolchain-pass1"
            }
          }
        }
      }
    }
    stage('Build Toolchain Stage 2') {
      steps {
        scripts {
          dir('container-build') {
            image.inside('-v $WORKSPACE:/target -u root') {
              sh "cd /home/docker/scripts"
              bash "01-toolchain-pass2"
            }
          }
        }
      }
    }
    stage('Collect Build Artifacts') {
      steps {
        scripts {
          dir('container-build') {
            image.inside('-v $WORKSPACE:/target -u root') {
              sh "cd /output;tar -czvf /target/toolchain-${env.BUILD_ID}.tar.gz lfs"
            }
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