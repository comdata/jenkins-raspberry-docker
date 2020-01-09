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
        deleteDir()

        stage('Checkout') {
            checkout scm
        }

        
        stage('Publish') {
            withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                sh './publish.sh --variant alpine'
            }
        }
    }
}

