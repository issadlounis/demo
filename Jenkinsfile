pipeline {

agent any
stages {

stage('init') {
steps {
bat 'mvn clean'
}
}

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
}
}

stage('documentation') {
steps {
bat 'mvn javadoc:javadoc'
bat '''
mkdir -p doc
cp -r target/site/* doc/
zip -r doc.zip doc
'''
archiveArtifacts artifacts: 'doc.zip'
}
}

}

}
