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
        sh 'mvn clean package'
        timeout(unit: 'HOURS', time: 1) {
          waitForQualityGate true
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