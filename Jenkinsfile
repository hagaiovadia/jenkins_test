pipeline {
    agent {
        label 'sonic-build'
    }
    stages {
      stage("speak") {
        steps {
          script {
            try {
              //Get the commiter email out of the repo
              COMMITER = sh (
                            script: 'git --no-pager show -s --format=\'%ce\'',
                            returnStdout: true
                            ).trim()

              print "COMMITER: ${COMMITER}"
              //Get slack user id from email
              USERID = slackUserIdFromEmail email: "${COMMITER}", botUser: true
              RESULT = currentBuild.currentResult
              messageColor = {
                if (RESULT == 'SUCCESS') return "#BADA55" else return "#FF2D00"
              }
              messageText = "[${RESULT}] UAT - ${currentBuild.displayName} by ${COMMITER}, Build Url: <http://test.com|test>"
              slackSend channel:"@${USERID},jenkins_delivery", color: "${messageColor}", message: "${messageText}", botUser: true, username: 'jenkinsbot'
            } catch (Exception e) {
                 print "Skipped slack step for message send"
            }
          } //script
        }
      }
    }
}
