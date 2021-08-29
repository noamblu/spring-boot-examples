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
        archiveArtifacts(onlyIfSuccessful: true, artifacts: '**/target/*.war')
      }
    }

    stage('Slack Notifcation') {
      steps {
        slackSend(message: '$JOB_NAME #BUILD_NUMBER - Started By $BUILD_USER ($BUILD_URL)', channel: 'noam-dev', color: '#008000')
        cleanWs(cleanWhenAborted: true, cleanWhenFailure: true, cleanWhenNotBuilt: true, cleanWhenSuccess: true, cleanWhenUnstable: true)
      }
    }

  }
}