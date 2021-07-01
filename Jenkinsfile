pipeline {
  agent any


  stages {
        stage('Build') {
      agent {
        docker {
          image 'gradle:7.1-jdk11'
          reuseNode true
        }
      }
      steps {
        sh 'gradle build --no-daemon'
      }
        }
  }

  post {
    always {
      archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
      junit '**/build/test-results/test/*.xml'
    }
  }

}
