pipeline {
  agent {
      dockerfile {
        filename 'Dockerfile'
        dir 'container-build'
        label 'toolchain'
        args '-v /tmp:/tmp'
    }
  }
  stages {
    stage('Building image') {
      steps{
        sh echo "BUILD COMPLETE!"
      }
    }
  }
}