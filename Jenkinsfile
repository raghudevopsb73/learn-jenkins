//pipeline {
//
//  agent { node { label 'workstation' } }
//
//  environment {
//    SSH = credentials('SSH')
//    DEMO_URL = "google.com"
//  }
//
//  options {
//    ansiColor('xterm')
//  }
//
//  triggers { pollSCM('H/2 * * * *') }
//
//  parameters {
//    string(name: 'APP_INPUT', defaultValue: '', description: 'Just Input')
//  }
//
//    stages {
//    stage('Hello-1') {
//      input {
//        message "Should we continue?"
//        ok "Yes, we should."
//      }
//      steps {
//        echo 'Hello World'
//        sh 'env'
//        sh 'echo APP_INPUT - $APP_INPUT'
//      }
//    }
//
//      stage('Example Deploy') {
//        when {
//          branch 'production'
//        }
//        steps {
//          echo 'Deploying'
//        }
//      }
//  }
//
//  post {
//    always {
//      sh 'echo Post'
//    }
//  }
//
//}
//
//// Comment
//


//pipeline {
//  agent any
//  stages {
//    stage('Non-Parallel Stage') {
//      steps {
//        echo 'This stage will be executed first.'
//      }
//    }
//    stage('Parallel Stage') {
//      failFast true
//      parallel {
//        stage('Branch A') {
//          agent {
//            label "for-branch-a"
//          }
//          steps {
//            echo "On Branch A"
//          }
//        }
//        stage('Branch B') {
//          agent {
//            label "for-branch-b"
//          }
//          steps {
//            echo "On Branch B"
//          }
//        }
//        stage('Branch C') {
//          agent {
//            label "for-branch-c"
//          }
//          stages {
//            stage('Nested 1') {
//              steps {
//                echo "In stage Nested 1 within Branch C"
//              }
//            }
//            stage('Nested 2') {
//              steps {
//                echo "In stage Nested 2 within Branch C"
//              }
//            }
//          }
//        }
//      }
//    }
//  }
//}


//properties([
//    parameters([
//        [
//            $class: 'ChoiceParameter',
//            choiceType: 'PT_SINGLE_SELECT',
//            name: 'Environment',
//            script: [
//                $class: 'ScriptlerScript',
//                scriptlerScriptId:'Environments.groovy'
//            ]
//        ],
//        [
//            $class: 'CascadeChoiceParameter',
//            choiceType: 'PT_SINGLE_SELECT',
//            name: 'Host',
//            referencedParameters: 'Environment',
//            script: [
//                $class: 'ScriptlerScript',
//                scriptlerScriptId:'HostsInEnv.groovy',
//                parameters: [
//                    [name:'Environment', value: '$Environment']
//                ]
//            ]
//        ]
//    ])
//])

//pipeline {
//  agent any
//  stages {
//    stage('Build') {
//      steps {
//        echo "${params.Environment}"
//        echo "${params.Host}"
//      }
//    }
//  }
//}


pipeline {
  agent any
  parameters {
    // Define the dropdown parameter
    choice(
        choices: getDropdownValues(), // Call a function to get dynamic values
        description: 'Select an option from the dropdown',
        name: 'DYNAMIC_DROPDOWN'
    )
  }
  stages {
    stage('Example Stage') {
      steps {
        // Your build steps go here
        echo "Selected option: \${params.DYNAMIC_DROPDOWN}"
      }
    }
  }
}

// Function to generate dynamic dropdown values
def getDropdownValues() {
  // Implement your logic here to generate dropdown values dynamically
  return ['Option 4', 'Option 2', 'Option 3']
}
