pipeline {
    agent {
        label 'sonic-build'
    }
    stages {
      stage("speak") {
        steps {
          slackSend color: '#BADA55', message: 'Hello, World!', channel: , notifyCommitters: true
        }
      }
    }
}
