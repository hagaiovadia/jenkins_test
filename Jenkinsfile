pipeline {
    agent {
        label 'sonic-build'
    }
    stages {
      stage("speak") {
        steps {
          print "GIT_AUTHOR_EMAIL: ${GIT_AUTHOR_EMAIL}"
          print "GIT_AUTHOR_EMAIL: ${GIT_COMMITTER_EMAIL}"
          slackSend channel:'@hagai.ovadia@ironsrc.com' color: '#BADA55', message: 'Hello, World!', botUser: true, notifyCommitters: true
        }
      }
    }
}
