def xcodepWorkspace = 'JenkinsTest.xcworkspace'
// def testBool() {
//     true
// }

pipeline {
    // def currentBranch = "${GIT_BRANCH}" 

    agent { label 'minibuilder'}

    // triggers {
    //      pollSCM('* * * * *')
    //  }

stages {

    stage('cocoapods') {
        steps {
            // sh '#!/bin/bash -l'
            sh 'gem install cocoapods'
            sh 'pod install' // cocoapods is used to manage our third-party dependencies
            }
        }

        stage('Build'){

            steps {
                echo 'Now Building...'
                // PATH+EXTRA='/usr/bin:/bin:/usr/sbin:/sbin'
                echo PATH
                sh "xcrun xcodebuild -workspace '${xcodepWorkspace}' -scheme JenkinsTest -configuration 'Debug' -sdk iphoneos CODE_SIGN_IDENTITY='' CODE_SIGNING_REQUIRED=NO clean build"
                
                //sh "xcodebuild -scheme JenkinsTest -workspace '${xcodepWorkspace}' archive"  
                // Pipe and xcpretty command can be omitted, | /usr/local/bin/xcpretty
                // if (${currentBranch} == 'origin/master') {
                //         echo 'Building succeeded....Olé..Oelala'
                //     }

                script {
                    if ("${env.BRANCH_NAME}" == 'origin/master') {
                        echo 'I only execute on the master branch'
                    } else {
                        echo 'I execute elsewhere'
                    }

                    // if (testBool) {
                    //     echo 'TESTBOO lDETECTED'
                    // }
                }
            }
            post {
                success {
                    echo "CURRENT BRANCH IS..."
                    // echo "${GIT_BRANCH}"
                    echo "${env.BRANCH_NAME}"
                }
            }
        }
        // stage('Upload') {
        //     steps {
        //         sh 'xcrun -sdk iphoneos PackageApplication -v JenkinsTest.app -o JenkinsTest.ipa --sign "iPhone Distribution: F Astitou"'
        //     }
        // }
    }
}
