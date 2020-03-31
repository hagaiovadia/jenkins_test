pipeline {
    agent {
        label 'sonic-build'
    }
    stages {
      stage("slack-send-message") {
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

              if (RESULT == 'SUCCESS') messageColor="#BADA55" else messageColor="#FF2D00"
              JOB_URL_SONIC = "http://sonic-ci.supersonic.com:8080/job/sonic-uat-pipeline/${BUILD_NUMBER}/display/redirect"
              messageText = "[${RESULT}] UAT - ${currentBuild.displayName} by ${COMMITER}, <${JOB_URL_SONIC}|Job Url>"
              slackSend channel:"@${USERID},jenkins_delivery", color: "${messageColor}", message: "${messageText}", botUser: true, username: 'jenkinsbot'
            } catch (Exception e) {
                 print "Skipped slack step for message send"
            }
          } //script
        }//steps
      }//stage
    }
}
