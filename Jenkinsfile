pipeline {
    agent any

    stages {
        // Phase Test - Lancement des tests unitaires et génération des rapports Cucumber lol
        stage('Test') {
            steps {
                script {
                    echo 'Lancement des tests unitaires...'
                    sh 'chmod +x gradle'
                    sh './gradlew test' // Exécute les tests unitaires avec Gradle
                }
            }
            post {
                always {
                    // Archivage des résultats des tests unitaires
                    junit '**/build/test-results/test/*.xml'
                    // Génération des rapports de tests Cucumber
                    cucumber '**/build/reports/cucumber/*.json'
                }
            }
        }
    }

    // Post-actions globales (par exemple, des notifications en cas d'échec)
    post {
        failure {
            script {
                echo 'Tests échoués. Envoi d’une notification d’échec.'
                // Logique pour envoyer des notifications d'échec si nécessaire
            }
        }
    }
}
