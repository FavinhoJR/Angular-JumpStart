pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv('sonarqube-local') {
          script {
            // Usa el nombre EXACTO de la herramienta en Global Tool: SonarScanner
            def scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
            bat "\"${scannerHome}\\bin\\sonar-scanner.bat\""
          }
        }
      }
    }
    stage('Quality Gate') {
      steps {
        timeout(time: 10, unit: 'MINUTES') {
          script {
            // En tu versión, este parámetro es requerido
            def qg = waitForQualityGate abortPipeline: false
            if (qg.status != 'OK') {
              error "Quality Gate FAILED: ${qg.status}"
            }
          }
        }
      }
    }
  }
}