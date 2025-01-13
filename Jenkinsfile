pipeline{
agent any





            stages {

                                stage('test') {
                                    steps {
                                        script {
                                            echo 'Tests en cours.....'
                                            sh './gradlew test'

                                        }


                                        }
                                        post {
                                            always {
                                                cucumber '**/reports/*.json'

                                            }
                                    }

                        }


                 }
}