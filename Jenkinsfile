pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/reports/tests/test'
      }
    }

  }
}