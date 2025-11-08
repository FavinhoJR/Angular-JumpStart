pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv('sonarqube-local') {
          def s = tool 'SonarScanner'   // Debe llamarse EXACTO así en Global Tool
          bat "\"%s%\\bin\\sonar-scanner.bat\""
        }
      }
    }
    stage('Quality Gate') {
      steps {
        timeout(time: 10, unit: 'MINUTES') {
          waitForQualityGate()
        }
      }
    }
  }
}