pipeline {
  agent none
  stages {
    stage("Build Toolchain") {
      agent {
        dockerfile {
          filename "container-build/Dockerfile"
          label "toolchain"
        }
      }
      steps {
        sh "tree /output/lfs"
      }
    }
  }
}