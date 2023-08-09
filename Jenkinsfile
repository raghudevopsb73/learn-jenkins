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


//pipeline {
//  agent any
//  parameters {
//    // Define the dropdown parameter
//    choice(
//        choices: getDropdownValues(), // Call a function to get dynamic values
//        description: 'Select an option from the dropdown',
//        name: 'DYNAMIC_DROPDOWN'
//    )
//  }
//  stages {
//    stage('Example Stage') {
//      steps {
//        // Your build steps go here
//        echo "Selected option: \${params.DYNAMIC_DROPDOWN}"
//      }
//    }
//  }
//}
//
//// Function to generate dynamic dropdown values
//def getDropdownValues() {
//  // Implement your logic here to generate dropdown values dynamically
//  return ['Option 4', 'Option 2', 'Option 3']
//}


//node('workstation') {
//
//    BRANCH_NAMES = sh (script: 'aws ecr describe-images --repository-name  frontend  --query \'imageDetails[*].imageTags\' --output text | sort ', returnStdout:true).trim()
//    print BRANCH_NAMES
//    //BRANCH_NAMES = sh (script: 'git ls-remote -h https://github.com/ansible/ansible | sed \'s/\\(.*\\)\\/\\(.*\\)/\\2/\' ', returnStdout:true).trim()
//}
//pipeline {
//
//  agent {
//      node {
//          label 'workstation'
//      }
//  }
//
//  parameters {
//    choice(
//        name: 'BranchName',
//        choices: "${BRANCH_NAMES}",
//        description: 'to refresh the list, go to configure, disable "this build has parameters", launch build (without parameters)to reload the list and stop it, then launch it again (with parameters)'
//    )
//  }
//
//  stages {
//    stage("Run Tests") {
//      steps {
//        sh "echo SUCCESS on ${BranchName}"
//      }
//    }
//  }
//}


//properties([
//    parameters([
//        [
//            $class: 'ChoiceParameter',
//            choiceType: 'PT_SINGLE_SELECT',
//            name: 'COMPONENT',
//            script: [
//                classpath: [],
//                sandbox: false,
//                script:
//                    '''
//                      def x = "/opt/aws-ecr-for-jenkins-param".execute()
//                      return x.in.text.tokenize()
//                    '''
//            ]
//        ],
//        [
//            $class: 'CascadeChoiceParameter',
//            choiceType: 'PT_SINGLE_SELECT',
//            name: 'Host',
//            referencedParameters: 'Environment',
//            script: [
//                classpath: [],
//                sandbox: false,
//                script:
//                    '''
//                      def x = "/opt/aws-ecr-for-jenkins-param".execute()
//                      return x.in.text.tokenize()
//                    ''',
//                parameters: [
//                    [name:'COMPONENT', value: '$COMPONENT']
//                ]
//            ]
//        ]
//    ])
//])

properties([
    parameters([
        [$class: 'ChoiceParameter',
         choiceType: 'PT_SINGLE_SELECT',
         description: 'Select the Env Name from the Dropdown List',
         filterLength: 1,
         filterable: true,
         name: 'Env',
         randomName: 'choice-parameter-5631314439613978',
         script: [
             $class: 'GroovyScript',
             fallbackScript: [
                 classpath: [],
                 sandbox: false,
                 script:
                     'return[\'Could not get Env\']'
             ],
             script: [
                 classpath: [],
                 sandbox: false,
                 script:
                     'return["Dev","QA","Stage","Prod"]'
             ]
         ]
        ],
        [$class: 'CascadeChoiceParameter',
         choiceType: 'PT_SINGLE_SELECT',
         description: 'Select the Server from the Dropdown List',
         filterLength: 1,
         filterable: true,
         name: 'Server',
         randomName: 'choice-parameter-5631314456178619',
         referencedParameters: 'Env',
         script: [
             $class: 'GroovyScript',
             fallbackScript: [
                 classpath: [],
                 sandbox: false,
                 script:
                     'return[\'Could not get Environment from Env Param\']'
             ],
             script: [
                 classpath: [],
                 sandbox: false,
                 script:
                     ''' if (Env.equals("Dev")){
                                return["devaaa001","devaaa002","devbbb001","devbbb002","devccc001","devccc002"]
                            }
                            else if(Env.equals("QA")){
                                return["qaaaa001","qabbb002","qaccc003"]
                            }
                            else if(Env.equals("Stage")){
                                return["staaa001","stbbb002","stccc003"]
                            }
                            else if(Env.equals("Prod")){
                                return["praaa001","prbbb002","prccc003"]
                            }
                        '''
             ]
         ]
        ]
    ])
])

pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo "${params.Environment}"
        echo "${params.Host}"
      }
    }
  }
}