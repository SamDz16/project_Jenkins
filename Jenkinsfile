pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        archiveArtifacts 'build/libs/*.jar'
        junit 'build/reports/tests/test/*.html'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Build Notification', body: 'This is a notification letting you know that the build stage has finished', to: 'hs_hendel@esi.dz', cc: 'hs_hendel@esi.dz')
      }
    }

  }
}