pipeline {
  agent any
  stages {
    stage('Build Toolchain') {
      steps {
        script {
          dir('container-build') {
            def image = docker.build("toolchain:${env.BUILD_ID}")
            image.inside('-v $WORKSPACE:/target -u root') {
              sh "cd /output;tar -czvf toolchain-$(env.BUILD_ID).tar.gz lfs"
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