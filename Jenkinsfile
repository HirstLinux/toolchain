pipeline {
  agent {
    docker {
      image 'hirstlinux/utility-image:latest'
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
        sh "cd build-scripts;bash 01-toolchain-pass1"
      }
    }
    stage('Build Toolchain Stage 2') {
      steps {
        sh 'echo null'
        sh "cd build-scripts;bash 01-toolchain-pass2"
      }
    }
    stage('Archive rootfs') {
      steps {
        sh 'echo null'
        sh "sudo chown root:root lfs/tools;cd lfs/tools;sudo tar -czvf ../../docker-build/toolchain.tgz ./*"
      }
    }
    stage('Build Docker Image') {
      agent node
      steps {
        dir("docker-build") {
          script{
            docker.withRegistry('https://registry.hub.docker.com', 'hirstlinux-docker') {
              def tcImage = docker.build("hirstlinux/toolchain:${env.BUILD_ID}")
              tcImage.push()
              tcImage.push('latest')
            }
          }
        }
      }
    }
  }
  //post {
    //success {
      //archiveArtifacts "toolchain.tgz"
    //}
  //}
}