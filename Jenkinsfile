pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                // Clone the repository
                
                echo 'Start Cloning'
                
                git branch: 'main', 
                    credentialsId: 'github',
                    url: 'https://github.com/Mohamed7Khalifa/Instabug.git',
                    tool: 'default'
                
                echo 'Done'
                
                // Use credentials to log in to Docker registry
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
