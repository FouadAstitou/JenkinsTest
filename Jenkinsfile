def xcodepWorkspace = 'JenkinsTest.xcworkspace'

pipeline {
    // def currentBranch = "${GIT_BRANCH}" 

    agent any //{ label 'minibuilder'}

    // triggers {
    //      pollSCM('* * * * *')
    //  }

stages{
        stage('Build'){

            steps {
                echo 'Now Building...'
                // PATH+EXTRA='/usr/bin:/bin:/usr/sbin:/sbin'
                echo PATH
                sh "xcrun xcodebuild -workspace '${xcodepWorkspace}' -scheme JenkinsTest -configuration 'Debug' -sdk iphoneos CODE_SIGN_IDENTITY='' CODE_SIGNING_REQUIRED=NO clean build"

                // Pipe and xcpretty command can be omitted, | /usr/local/bin/xcpretty
                // if (${currentBranch} == 'origin/master') {
                //         echo 'Building succeeded....Olé..Oelala'
                //     }

                script {
                    if ("${GIT_BRANCH}" == 'origin/master') {
                        echo 'I only execute on the master branch'
                    } else {
                        echo 'I execute elsewhere'
                    }
                }
            }
            post {
                success {
                    echo "CURRENT BRANCH IS..."
                    echo "${GIT_BRANCH}"
                    echo "${env.BRANCH_NAME}"
                }
            }
        }
    }
}
