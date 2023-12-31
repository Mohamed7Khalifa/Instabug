pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                script {
                    try {
                        // Clone the repository
                        echo 'Start Cloning'
                        git url: 'https://github.com/Mohamed7Khalifa/Instabug.git', credentialsId: 'Github', branch: 'main'

                        echo 'Done'
                        
                        // Use credentials to log in to Docker registry
                        withCredentials([usernamePassword(credentialsId: 'Docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                            sh """
                            docker login -u ${USERNAME} -p ${PASSWORD}
                            docker build -t mohamed7khalifa/api-app ./internship/
                            docker push mohamed7khalifa/api-app
                            """
                        }
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        env.ERROR_MESSAGE = e.getMessage()
                        error "Build failed: ${e.getMessage()}"
                    }
                }
            }
        }
    }

    post {
        always {
            // Report the build result to Slack
            slackSend(channel: '#api', message: "Build Status: ${currentBuild.result}")
        }

        failure {
            // Report to Slack if the build fails
            slackSend(channel: '#api', message: "Build failed with error: ${env.ERROR_MESSAGE}")
        }
    }
}
