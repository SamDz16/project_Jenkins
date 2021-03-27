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
        mail(subject: 'Build Finished', body: 'This is a notification letting you know that the build stge has finished being executing', from: 'hs_hednel@esi.dz', to: 'hs_hendel@esi.dz')
      }
    }

  }
}