pipeline {
    environment {
        registry = "comdata456/jenkins-raspberry"
        registryCredential = 'docker-hub-credentials'
    }

    agent {
        docker {
            image 'docker'
            args '-v $HOME/.m2:/root/.m2 -v /root/.ssh:/root/.ssh -v /run/docker.sock:/run/docker.sock'
        }
    }



    stages {
 
         stage('Prepare') {
            steps {
                //sh 'apt-get update'
                //sh 'apt-get install -y apt-transport-https ca-certificates curl gnupg software-properties-common'
                //sh 'curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -'
                //sh 'apt-key fingerprint 0EBFCD88'
                //sh 'add-apt-repository "deb [arch=armhf] https://download.docker.com/linux/debian $(lsb_release -cs) stable"'
                //sh 'apt-get update'
                //sh 'apt-get install -y bash docker-ce:armhf docker-ce-cli:armhf containerd.io:armhf'
                sh 'which docker'
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
                    sh 'docker login -u ${USERNAME} -p ${PASSWORD}'
                    sh 'make publish'
                }
            }
        }
    }
}