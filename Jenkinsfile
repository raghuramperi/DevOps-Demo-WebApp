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
      }
    }

    stage('Compile Webapp') {
      steps {
        echo 'Compiling Webapp'
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