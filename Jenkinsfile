pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                git 'https://github.com/'
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh """
                docker login -u ${USERNAME} -p ${PASSWORD}
                docker build . -t mohamed7khalifa/inernship --network host
                docker push mohamed7khalifa/inernship
                """
                }
            }
        }
    }
}