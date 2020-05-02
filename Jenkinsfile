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
        sh 'pwd'
        sh 'tree .'
        //sh 'sudo mkdir -p /output/lfs /output/lfs/tools'
        //sh 'git clone https://github.com/HirstLinux/toolchain.git /home/docker/scripts'
        //sh 'cd /home/docker/scripts'
        //sh 'version-check.sh'
      }
    }
    stage('Build Toolchain Stage 1') {
      steps {
        sh 'echo null'
        //sh "cd /home/docker/scripts;./01-toolchain-pass1"
      }
    }
    stage('Build Toolchain Stage 2') {
      steps {
        sh 'echo null'
        //sh "cd /home/docker/scripts;./01-toolchain-pass2"
      }
    }
  }
  post {
    always {
      archiveArtifacts "$WORKSPACE/lfs"
    }
  }
}