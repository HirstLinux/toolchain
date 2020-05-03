pipeline {
  agent {
    docker {
      image 'hirstlinux/utility-image:2'
      }
    }
  stages {
    stage('Prepare docker workspace') {
      steps {
        sh 'bash version-check.sh;mkdir -p $WORKSPACE/lfs/tools;sudo ln -s $WORKSPACE/lfs/tools /tools;ls -alF /tools;sudo chown -R docker $WORKSPACE/lfs'
      }
    }
    stage('Build Toolchain Stage 1') {
      steps {
        sh 'echo null'
        sh "cd lfs-scripts;bash 01-toolchain-pass1"
      }
    }
    stage('Build Toolchain Stage 2') {
      steps {
        sh 'echo null'
        sh "cd lfs-scripts;bash 01-toolchain-pass2"
      }
    }
  }
  post {
    always {
      archiveArtifacts "lfs/tools/**/*.*"
    }
  }
}