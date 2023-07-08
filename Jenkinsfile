pipeline {

  agent { node { label 'workstation' } }

  environment {
    SSH = credentials('SSH')
    DEMO_URL = "google.com"
  }

  options {
    ansiColor('xterm')
  }

  triggers { pollSCM('H/2 * * * *') }

  parameters {
    string(name: 'APP_INPUT', defaultValue: '', description: 'Just Input')
  }

    stages {
    stage('Hello-1') {
      input {
        message "Should we continue?"
        ok "Yes, we should."
      }
      steps {
        echo 'Hello World'
        sh 'env'
        sh 'echo APP_INPUT - $APP_INPUT'
      }
    }

      stage('Example Deploy') {
        when {
          branch 'production'
        }
        steps {
          echo 'Deploying'
        }
      }
  }

  post {
    always {
      sh 'echo Post'
    }
  }

}

// Comment

