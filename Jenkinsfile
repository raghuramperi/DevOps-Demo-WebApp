pipeline {
  agent any
  //defone tools maven,artifactory,kubernetes etc..global config..
  rtMaven.tool = "maven"
  stages {
    stage('Clone Webapp') {
      steps {
        git(url: 'https://github.com/raghuramperi/DevOps-Demo-WebApp.git')
      }
    }

    stage('Static Code Analysis') {
      steps {
        echo 'Code Analysis using Sonar Qube'
        withSonarQubeEnv(installationName: 'sonarqube', credentialsId: 'sonar')
        sh 'mvn clean package'
            sonar:sonar -Dsonar.host.url:http://104.42.51.111//
            -Dsonar.sources=. -Dsonar.tests=. -Dsonar.test.inclusions
            timeout(time: 1, unit: 'HOURS')
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
        deploy adapters:[tomcat8(credentialsId: 'tomcat',path: '',url: 'http://')],contextpath: '/QAWebapp',
      }
    }

    stage('Storing Artifacts') {
      steps {
        echo 'Storing Artifacts'
      }
    }

  }
}
