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
        
        
                 }
}
