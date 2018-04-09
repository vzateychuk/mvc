node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get the Maven tool.
      mvnHome = tool 'MAVEN3'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.war'
   }
   stage('deployToDev') {
        sh 'cp ./target/mvc*.war $CATALINA_HOME/webapps/mvc.war'
        sh 'sleep 20'
   }
      stage('complete') {
          sh 'echo Completed ${BRANCH_NAME}...'
      }
}
