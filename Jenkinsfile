pipeline {

agent any
stages {

stage('build') {

steps {
bat 'mvn clean package'
archiveArtifacts 'target/*.jar'
junit 'target/surefire-reports/*.xml'
}

}
}

}
