pipeline {
  agent {
    node {
      label 'ubuntu-slave'
    }

  }
  stages {
    stage('CheckOut Code') {
      steps {
        git(url: 'https://github.com/noamblu/spring-boot-examples.git', branch: 'noam_sol', credentialsId: 'GitHub')
      }
    }

    stage('Maven Bulid') {
      steps {
        sh '''cd spring-boot-package-war/
mvn versions:set -DnewVersion=0.0.$BUILD_NUMBER-SNAPSHOT
mvn package
'''
      }
    }

  }
}