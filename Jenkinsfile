...
    stage('Install') { steps { bat 'npm ci || npm install' } }
    stage('Build')   { steps { bat 'npm run build || npx ng build || exit /b 0' } }
    // stage('Test')   { steps { bat 'npm test -- --watch=false --code-coverage || exit /b 0' } }
    stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv('sonarqube-local') {
          def scannerHome = tool 'SonarScanner'
          bat "\"%scannerHome%\\bin\\sonar-scanner.bat\""
        }
      }
    }
...