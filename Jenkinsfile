pipeline {
    agent any
 tools {
    maven 'localMAVEN'
    //Test
 }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                echo 'Now Building...'

                // Pipe and xcpretty command can be omitted
                xcrun xcodebuild -workspace InnovatieApp.xcworkspace \
                -scheme InnovatieApp \
                -configuration "Debug" \
                -sdk iphoneos \
                CODE_SIGN_IDENTITY="" CODE_SIGNING_REQUIRED=NO \
                clean build | /usr/local/bin/xcpretty 
            }
            post {
                success {
                    echo 'Building succeeded....'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        // stage ('Deployments'){
        //     parallel{
        //         stage ('Deploy to Staging'){
        //             steps { 
        //                 sh "scp -i /Users/fouadastitou/Downloads/TomcatStaging.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
        //             }
        //         }

        //         stage ("Deploy to Production"){
        //             steps {
        //                 sh "scp -i /Users/Shared/Jenkins/.ssh/TomcatProd.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
        //             }
        //         }
        //     }
        // }
    }
}
