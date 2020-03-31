pipeline {
    agent {
        label 'sonic-build'
    }

    post {
        always {
          sendSlackMessageStage()
       } //always
     } //post

}

def sendSlackMessageStage() {
  return {
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

        JOB_URL_SONIC = "${env.BUILD_URL}/display/redirect"
        REBUILD_URL = "${env.BUILD_URL}rebuild/parameterized"
        messageText = "[${RESULT}] UAT - ${currentBuild.displayName}, duration:  ${currentBuild.durationString.replace(' and counting', '')}, <${JOB_URL_SONIC}|Job Url>, <${REBUILD_URL}|Rebuild>, commiter: ${COMMITER}"

        slackSend channel:"@${USERID},jenkins_delivery", color: "${messageColor}", message: "${messageText}", botUser: true, username: 'jenkinsbot'
      } catch (Exception e) {
           print "Skipped slack step for message send"
      }
    } //script
  }//return
}
