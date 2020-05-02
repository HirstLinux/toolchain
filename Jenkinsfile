pipeline {
  agent {
    docker {
      image 'hirstlinux/utility-image:2'
      args '-v $WORKSPACE:/output'
      }
    }
  stages {
    stage('Prepare docker workspace') {
      steps {
        sh 'version-check.sh'
      }
    }
    stage('Build Toolchain Stage 1') {
      steps {
        sh "cd lfs-scripts;./01-toolchain-pass1"
      }
    }
    stage('Build Toolchain Stage 2') {
      steps {
        sh "cd lfs-scripts;./01-toolchain-pass1"
      }
    }
  }
  post {
    always {
      archiveArtifacts "$WORKSPACE/lfs"
    }
  }
}