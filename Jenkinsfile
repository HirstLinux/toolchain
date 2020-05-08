pipeline {
  agent any
  stages {
    stage('Steps to execute in docker agent') {
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
            sh "sudo chown -R root:root $WORKSPACE/lfs/tools;cd $WORKSPACE/lfs/tools;sudo rm -rf ./[0-9]*;sudo tar -czpvf $WORKSPACE/docker-build/toolchain.tgz ./*"
          }
        }
      }
    }
    stage('Build Docker Image') {
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