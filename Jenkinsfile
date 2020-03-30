pipeline {
    agent {
        label 'sonic-build'
    }
    stages {
      stage("speak") {
        steps {
          script {
            print "GIT_AUTHOR_EMAIL: ${GIT_AUTHOR_EMAIL}"
            print "GIT_AUTHOR_EMAIL: ${GIT_COMMITTER_EMAIL}"
            //UPWK0HDST
            //hagai.ovadia@ironsrc.com
            COMMITER = sh "git log -1 --pretty='format:%cE'"
            print "COMMITER: ${COMMITER}"
            USERID = slackUserIdFromEmail email: "#{COMMITER}", botUser: true
            print "USERID: ${USERID}"

            slackSend channel:'@UPWK0HDST', color: '#BADA55', message: 'Hello, World!', botUser: true, notifyCommitters: true
          } //script
        }
      }
    }
}
