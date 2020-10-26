pipeline {
  agent any
  stages {
    stage('Clone Webapp') {
      steps {
        git(url: 'https://github.com/raghuramperi/DevOps-Demo-WebApp.git', poll: true)
      }
    }

    stage('Static Code Analysis') {
      steps {
        echo 'Code Analysis using Sonar Qube'
        withSonarQubeEnv(installationName: 'sonarqube', credentialsId: 'sonar')
        sh 'mvn clean package
            sonar:sonar -Dsonar.host.url://http://23.101.202.169//
            -Dsonar.sources=. -Dsonar.tests=. -Dsonar.test.inclusions'
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
