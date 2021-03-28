pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/**'
        junit 'build/test-results/test/*.xml'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Build Notification', body: 'This is a notification letting you know that the build stage has finished', to: 'hs_hendel@esi.dz', cc: 'samdz161999@gmail.com', from: 'hs_hendel@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarQube'
            }

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

    stage('Deployment') {
      steps {
        bat 'gradle publish'
      }
    }

    stage('Slack Notification') {
      steps {
        slackSend(baseUrl: 'https://hooks.slack.com/services', channel: '#projet', notifyCommitters: true, sendAsText: true, username: 'SAMY HENDEL', message: 'This is a slack notification letting you know that he process has finished ', replyBroadcast: true, teamDomain: 'https://app.slack.com/client', token: 'T01SJTB0CQ5/B01S7A6BKAB/sO1DfcByynE2Wz12LBoy00ip')
      }
    }

  }
}