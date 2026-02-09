pipeline {

agent any
    stages {

        stage('init') {
            steps {
                bat 'mvn clean'
            }
        }
        /*
        stage('test') {
            steps {
                bat 'mvn test'
                archiveArtifacts 'target/surefire-reports/*.xml'
            }
        }

        stage('build') {
            steps {
                bat 'mvn clean package'
                archiveArtifacts 'target/*.jar'
            }*/
            /*
            post {
                always {
                    echo "Build stage complete"
                }

                failure {
                            mail(subject: "Build réussi: ",
                                    body: "Le build a échoué.",
                                    to: "louniscntsid@gmail.com"
                                    )
                }

                success {
                           mail(subject: "Build réussi: ",
                                   body: "Le build a réussi.",
                                   to: "louniscntsid@gmail.com"
                                   )
                }
            }
            */

        //}

        stage('Build & Test in Parallel') {
            parallel {
                stage('Build') {
                    steps {
                        bat 'mvn clean package'
                    }
                }

                stage('Test') {
                    steps {
                        bat 'mvn test'
                    }
                }
            }
        }

        stage('documentation') {
            steps {
                bat 'mvn javadoc:javadoc'
                /*bat 'powershell Compress-Archive -Path target/site/* -DestinationPath target/doc.zip'
                archiveArtifacts artifacts: 'target/doc.zip'*/
            }
        }

        stage('publish report') {
            steps {

                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'target/site/apidocs',
                    reportFiles: 'index.html',
                    reportName: 'Documentation'
                ])

            }
        }

        stage('deployment') {
            steps {
                bat 'docker-compose up --build -d'
            }
        }

    }
}
