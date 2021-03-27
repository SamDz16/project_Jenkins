pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        javadoc(javadocDir: 'Docs', keepAll: true)
      }
    }

  }
}