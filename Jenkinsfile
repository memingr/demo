pipeline {
  agent {
        docker {
            image 'openjdk:11'
            args '-v "$PWD":/app'
            reuseNode true
        }
    }
    
  stages {
    stage('Unit & Integration Tests') {
      steps {
        script {
          sh './gradlew clean build --no-daemon' //run a gradle task
        }
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
