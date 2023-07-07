pipeline {

  agent { node { label 'workstation' } }

  stages {
    stage('Hello-1') {
      steps {
        echo 'Hello World'
      }
    }
  }

  post {
    always {
      sh 'echo Post'
    }
  }

}

