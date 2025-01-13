


pipeline {
    agent any 

    environment {
        MAVEN_REPO_USERNAME = credentials('myRandomID_34892')
        MAVEN_REPO_PASSWORD = credentials('myRandomID_34892')
    }

    stages {
        // Étape pour exécuter les tests
        stage('test') {
            steps {
                script {
                    echo 'Execution des tests...'
                    sh 'chmod +x gradle'
                    sh './gradlew test'
                }
            }
            post {
                always {
                    cucumber '**/reports/*.json'
                }
            }
        }
        
         post {
        always {
            echo 'Pipeline termine.'
        }
        success {
            echo 'Pipeline complete avec succes.'
        }
        failure {
            echo 'Le pipeline a echoue.'
        }
    }
}