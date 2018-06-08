def xcodepWorkspace = 'JenkinsTest.xcworkspace'
// def testBool() {
//     true
// }

pipeline {
    // def currentBranch = "${GIT_BRANCH}" 

    agent { label 'MacMini'}

    // triggers {
    //      pollSCM('* * * * *')
    //  }

stages {

    stage('cocoapods') {
        steps {
            // sh 'gem install -n /usr/local/bin cocoapods'
            // sh 'gem install -n /usr/local/bin xcpretty' //[Use this to install gems in a way they can be found by the system]
            echo 'Pod instal....'
            sh 'pod install' // cocoapods is used to manage our third-party dependencies
            }
        }

        stage('Build'){

            steps {
                echo 'Now Building...'
                // PATH+EXTRA='/usr/bin:/bin:/usr/sbin:/sbin'
                echo PATH
                sh "xcrun xcodebuild -workspace '${xcodepWorkspace}' -scheme JenkinsTest -configuration 'Debug' -sdk iphoneos CODE_SIGN_IDENTITY='' CODE_SIGNING_REQUIRED=NO clean build | xcpretty"
                // sh "xcrun xcodebuild -workspace '${xcodepWorkspace}' -scheme JenkinsTest -configuration 'Debug' -sdk iphoneos CODE_SIGN_IDENTITY='' CODE_SIGNING_REQUIRED=NO archive | xcpretty"
                // sh 'xcodebuild -workspace JenkinsTest.xcworkspace -scheme JenkinsTest -sdk iphoneos -configuration AppStoreDistribution archive -archivePath $PWD/build/JenkinsTest.xcarchive'
                // sh "xcodebuild -scheme JenkinsTest -workspace '${xcodepWorkspace}' archive | xcpretty"  
                // Pipe and xcpretty command can be omitted, | /usr/local/bin/xcpretty
                // if (${currentBranch} == 'origin/master') {
                //         echo 'Building succeeded....Olé..Oelala'
                //     }
                // 

                script {
                    if (env.BRANCH_NAME == 'origin/master') {
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
                    sh "agvtool new-marketing-version 2.0"
                }
            }
        }

        stage('export') {
            steps {
                // sh 'xcrun -sdk iphoneos PackageApplication -v JenkinsTest.app -o JenkinsTest.ipa --sign "iPhone Distribution: F Astitou"'
                // sh 'xcodebuild -exportArchive -archivePath $PWD/build/JenkinsTest.xcarchive -exportOptionsPlist ExportOptions.plist -exportPath $PWD/build'
            }
        }

        stage('upload') {
            steps {
                sh 'cd build'
                // sh '/Applications/Xcode.app/Contents/Applications/Application\ Loader.app/Contents/Frameworks/ITunesSoftwareService.framework/Support/altool --upload-app -f "JenkinsTest.ipa" -u f.astitou@gmail.com'
            }
        }
    }
}
