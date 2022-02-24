pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/bnasslahsen/ddd-sample.git', credentialsId: 'git-login', branch: 'master')
      }
    }
    stage('Compile') {
      steps {
       withMaven(maven: 'maven') {
          bat 'mvn clean compile'
        }

      }
    }
    stage('Test') {
      steps {
        withMaven(maven: 'maven') {
          bat 'mvn test'
        }

      }
    }
    stage('Package') {
      steps {
       withMaven(maven: 'maven') {
          bat 'mvn package -DskipTests'
        }

      }
    }

   stage('Quality') {
      steps {
       withSonarQubeEnv('Sonar-ddd') {
          bat 'mvn sonar:sonar'
        }
    }
   }
 }
}
