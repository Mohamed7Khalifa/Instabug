pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                git 'https://github.com/Mohamed7Khalifa/Instabug.git'
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh """
                docker login -u ${USERNAME} -p ${PASSWORD}
                docker build ./internship/ -t mohamed7khalifa/api-app
                docker push mohamed7khalifa/api-app
                """
                }
            }
        }
    }
}
