stage('Build') {
    node {
        git url: 'https://github.com/vzateychuk/mvc.git'
        env.PATH = "${tool 'MAVEN3'}/bin:${env.PATH}"
        sh 'mvn clean package'
        archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
        sh 'sleep 10'
    }
}

stage('SonarQube analysis') {
    node {
        withSonarQubeEnv('sonar') {
            env.PATH = "${tool 'MAVEN3'}/bin:${env.PATH}"
            sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
            sh 'sleep 10'
        }
    }
}

stage('deployToDev') {
    node {
        sh 'cp "./target/mvc2.war" $CATALINA_HOME/webapps'
        sh 'sleep 20'
    }
}
