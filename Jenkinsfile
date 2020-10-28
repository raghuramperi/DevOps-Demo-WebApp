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
           mvn "$SONAR_MAVEN_GOAL -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=$SONAR_AUTH_TOKEN "
         
          }
        timeout(unit: 'MINUTES', time: 20) {
           def qg = waitForQualityGate()
          if(qg.status != 'OK') { 
            error "Pipeline aborthed due to quality gate failure: ${qg.status}"
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

    stage('Deploy to Test') {
      steps {
        echo 'Deploy to Tomcat Server in Test Environment'
      }
    }

    stage('Storing Artifacts') {
      steps {
        echo 'Storing Artifacts'
      }
    }

  }
}
