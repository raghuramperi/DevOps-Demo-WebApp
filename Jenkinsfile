pipeline {
  agent any
  stages {
    stage('Clone Webapp') {
      steps {
        git 'https://github.com/raghuramperi/DevOps-Demo-WebApp.git'
      }
    }
    stage('Static Code Analysis') {
      steps {
        echo 'Code Analysis using Sonar Qube'
        withSonarQubeEnv(installationName: 'sonarqube', credentialsId: 'sonar')
        
        {
          withSonarQubeEnv(credentialsId: 'sonar-test', installationName: 'sonarqube') { // You can override the credential to be used
       		sh 'mvn clean package 
          sonar:sonar -Dsonar.host.url=http://104.42.192.90// -Dsonar.sources=. -Dsonar.tests=. -Dsonar.test.inclusions=**/test/java/servlet/createpage_junit.java 
            -Dsonar.exclusions=**/test/java/servlet/createpage_junit.java'
          }
 
         timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
	       def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
	       if (qg.status != 'OK') {
	        error "Pipeline aborted due to quality gate failure: ${qg.status}"
	    }
	}      
      }
    }

    stage('Compile Webapp') {
      steps {
        echo 'Compiling Webapp'
        sh 'mvn compile'
      }
    }
  }
}

   
