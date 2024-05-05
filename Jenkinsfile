pipeline {
  agent any
  tools {
    // EN: We use the previously defined node installation. This adds node to the PATH as well
    nodejs 'nodejs'
  }
  environment {
    scannerHome = tool name: 'sonar-scanner'
  }
  stages {
    stage('Scan') {
      steps {
        withSonarQubeEnv(installationName: 'sonarQube') { 
          sh '${scannerHome}/bin/sonar-scanner'
        }
      }
    }
    
    stage('Wait for quality Gate') {
      steps {
        timeout(time: 2, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }  
      }
    }
  }
}
