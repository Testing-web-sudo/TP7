pipeline{
agent any





    
            stages {
         

                                stage('test') {
                                    steps {
                                        script {
                                            echo 'Tests en cours.....'

                                            bat './gradlew test'
                        
                                        }
                        

                                        }
                                        post {
                                            always {
                                                cucumber '**/reports/*.json'

                        
                                            }
                                    }
                        
                           }

                           stage('AnalyseCode') {


                                       steps {
                                           script {
                                               echo 'Analyse Sonarqube en cours...'
                                               withSonarQubeEnv('sonar') {
                                                   bat './gradlew sonarqube'
                                               }
                                           }
                                       }
                                   }

                             stage('QualityGate') {
                                                         steps {
                                                            script {
                                                                echo 'SonarQube Quality Gate Test en cours...'
                                                               def qualityGate = waitForQualityGate()
                                                                 if (qualityGate.status != 'OK') {
                                                                     error "echec dans SonarQube Quality Gate : ${qualityGate.status}"
                                                                }
                                                            }
                                                        }
                                                    }


                                                    stage('Build') {
                                                        steps {
                                                            script {
                                                                echo 'Build du projet...'

                                                                bat './gradlew build'
                                                            }
                                                        }
                                                    }

                                 stage('ArchiverArtifacts') {
                                            steps {
                
                                                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
                                                archiveArtifacts artifacts: 'build/reports/tests/**/*', fingerprint: true
                                                archiveArtifacts artifacts: 'build/reports/cucumber/**/*', fingerprint: true
                                            }
                                        }

                stage('Deploy') {
                                    steps {
                                        script {
                                            echo 'Deploiement de le application...'
                                            sh './gradlew publish'
                                        }
                                    }
                                }

            
        




           }
}

