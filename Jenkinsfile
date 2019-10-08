node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/adptraining1/cd-demo-customer.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage("Sonar Qube") {
       def scannerHome = tool 'SonarQube Scanner 3.0';
        withSonarQubeEnv('Local SonarQube') {
            sh "${scannerHome}/bin/sonar-scanner"
        }
       
   }
   stage('Results') {
      archive 'target/*.jar'
   }
}