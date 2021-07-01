pipeline {
  agent any

  stages {
    stage('Unit & Integration Tests') {
      steps {
        script {
          sh './gradlew clean build --no-daemon' //run a gradle task
        }
      }
    }
  }

  stages {
        stage('Build') {
      agent {
        docker {
          image 'gradle:7.1-jdk11'
          reuseNode true
        }
      }
      steps {
        sh 'gradle clean build'
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
