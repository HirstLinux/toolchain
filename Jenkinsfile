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
    stage('Clone repository') {
      checkout scm
    }
    stage('Build image') {
        app = docker.build("hirstlinux/toolchain")
    }
    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */
        app.inside {
            sh 'echo "Tests passed"'
        }
    }
    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'hirstlinux-docker') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
  }
}