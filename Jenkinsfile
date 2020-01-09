pipeline {
    environment {
        registry = "comdata456/jenkins-raspberry"
        registryCredential = 'docker-hub-credentials'
    }

    agent {
        docker {
            image 'debian'
            args '-v $HOME/.m2:/root/.m2 -v /root/.ssh:/root/.ssh -v /run/docker.sock:/run/docker.sock -v /usr/bin/docker:/usr/bin/docker'
        }
    }



    stages {
 
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        
        stage('Publish') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                    sh 'make publish'
                }
            }
        }
    }
}

