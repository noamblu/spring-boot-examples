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

    stage('Maven Compile') {
      steps {
        sh '''cd spring-boot-package-war/
mvn versions:set -DnewVersion=0.0.$BUILD_NUMBER-SNAPSHOT
mvn compile
'''
      }
    }

    stage('Maven Test') {
      steps {
        sh '''cd spring-boot-package-war/
mvn test'''
      }
    }

    stage('Maven Package') {
      steps {
        sh '''cd spring-boot-package-war/
mvn clean package'''
      }
    }

    stage('Archive the artifacts') {
      steps {
        archiveArtifacts(onlyIfSuccessful: true, artifacts: 'packege.zip')
      }
    }

    stage('Slack Notifcation') {
      steps {
        slackSend(message: 'The bulis is finsh OK', channel: 'noam-dev')
      }
    }

  }
}