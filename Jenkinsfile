pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        javadoc(javadocDir: 'build/docs', keepAll: true)
        archiveArtifacts 'build/libs/*.jar'
        junit 'build/reports/tests/test/*.html'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Build Notification', body: 'This is a notification letting you know that the build stage has finished', to: 'samdz161999@gmail.com', cc: 'samdz161999@gmail.com', from: 'hs_hendel@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv 'build/sonar/report-task.txt'
            waitForQualityGate true
          }
        }

        stage('Test Reporting') {
          steps {
            cucumber 'reports/example-report.json'
          }
        }

      }
    }

  }
}