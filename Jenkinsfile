pipeline {
  agent any
  stages {
    stage('CheckOut Code') {
      steps {
        git(url: 'https://github.com/noamblu/spring-boot-examples.git', branch: 'noam_sol', credentialsId: 'GitHub')
      }
    }

    stage('Maven Bulid') {
      steps {
        sh '''mvn package
'''
      }
    }

  }
}