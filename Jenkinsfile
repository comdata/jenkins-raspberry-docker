pipeline {
    triggers {
        cron('H 4 * * *')
        pollSCM('H */4 * * 1-5')
    }

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
                sh 'apk update'
                sh 'apk add make bash curl'
            }
        }

/*        stage('Checkout') {
            steps {
                checkout scm
            }
        }*/

        
        stage('Publish') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'docker login -u ${USERNAME} -p ${PASSWORD}'
                    sh 'chmod 755 publish.sh'
                    sh 'make publish'
                }
            }
        }
    }
}