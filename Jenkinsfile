pipeline {
    agent any
    
    tools {
        // Must match the name you gave the scanner in 'Global Tool Configuration'
        sonarScanner 'SonarScanner'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // 'SonarServer' must match the name in 'Configure System'
                withSonarQubeEnv('SonarServer') {
                    sh 'sonar-scanner'
                }
            }
        }

        stage("Quality Gate") {
            steps {
                // Pauses until SonarQube sends back a pass/fail result
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}

