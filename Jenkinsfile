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
/*bat 'powershell Compress-Archive -Path target/site/* -DestinationPath target/doc.zip'
archiveArtifacts artifacts: 'target/doc.zip'*/

}

post {
    always {
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
}

}
}
