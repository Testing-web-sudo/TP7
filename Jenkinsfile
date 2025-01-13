pipeline {
    agent any

    environment {
        MAVEN_REPO_USERNAME = credentials('Testing-web-sudo')
        MAVEN_REPO_PASSWORD = credentials('Testing-web-sudo')
    }

    stages {
        // Stage to execute tests
        stage('Test') {
            steps {
                script {
                    echo 'Executing tests...'
                    sh 'gradle test'
                }
            }
            post {
                always {
                    junit '**/build/test-*.xml' // Archive JUnit test results
                    cucumber '**/build/reports/cucumber/*.json' // Archive Cucumber reports
                }
            }
        }

        // Stage for code analysis (SonarQube)
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Running SonarQube analysis...'
                    withSonarQubeEnv('sonar') {
                        sh 'gradle sonarqube' // Running SonarQube analysis
                    }
                }
            }
        }

        // Stage to verify code quality (SonarQube Quality Gate)
        stage('Code Quality') {
            steps {
                script {
                    echo 'Checking SonarQube Quality Gate...'
                    def qualityGate = waitForQualityGate()  // Wait for the quality gate status
                    if (qualityGate.status != 'OK') {
                        error "SonarQube Quality Gate failed: ${qualityGate.status}"  // Fail the pipeline if quality gate fails
                    }
                }
            }
        }
    }
}
