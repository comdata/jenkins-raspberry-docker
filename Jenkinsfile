pipeline {
    environment {
        registry = "comdata456/jenkins-raspberry"
        registryCredential = 'docker-hub-credentials'
    }

    agent {
        docker {
            image 'debian'
            args '-v $HOME/.m2:/root/.m2 -v /root/.ssh:/root/.ssh -v /run/docker.sock:/run/docker.sock'
        }
    }



    stages {
 
         stage('Prepare') {
            steps {
                sh 'apt-get update'
                sh 'apt-get install -y bash docker'
            }
        }

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        
        stage('Publish') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh '/usr/bin/docker login -u ${USERNAME} -p ${PASSWORD}'
                    sh 'make publish'
                }
            }
        }
    }
}

