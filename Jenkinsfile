pipeline {

    agent any




    stages {

        stage('Build') {

        when {  not { branch 'main'} }

         

            steps {

                cleanWs()

                echo 'Building..'

            }

        }

        stage('Sonar Scan') {

        when {  allOf{

                      not { branch 'release'}

                      not { branch 'main'}

                      not { branch 'staging'}




                }

            }

         

            steps {

                echo 'Building..'

            }

        }

        stage('Run Test cases') {

            when {

                anyOf{

                      changeRequest()

                      not { branch 'main'}




                }

                }

            steps {

                echo 'Running Test cases..'

            }

        }

        stage('Upload To AppCenter') {

        when {  

            allOf{

                not { branch 'main'}

                not {changeRequest()}

            }

        }

         

            steps {

                echo 'uploading to appcenter..'

            }

        }

        stage('Upload To Nexus') {

        when {

            allOf{

                not { branch 'main'}

                not {changeRequest()}

            }

            

         }

         

            steps {

                echo 'uploading to Nexus..'

            }

        }

        stage('Download from nexus') {

        when {   branch 'main'}

         

            steps {

                echo 'Downloading from nexus..'

            }

        }

        stage('Deploy to Appstore') {

            when {

                    branch 'main'

            }

            steps {

                timeout(time: 15, unit: "MINUTES") {

                        input message: 'Do you want to approve the deployment?', ok: 'Yes'

                    }

                echo 'Deploying....'

            }

        }

    }

    post {

    always {

            echo 'One way or another, I have finished'

            deleteDir() /* clean up our workspace */

        }

    success {

            echo 'I succeeded!'

        }

    unstable {

            echo 'I am unstable :/'

        }

    failure {

            echo 'I failed :('

        }

    }

}