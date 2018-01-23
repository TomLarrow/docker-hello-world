pipeline {
    agent { node { label 'master' }}

    stages {
        stage ('prepare'){
            steps{
                sh "ls -al"
            }
        }
        stage ('docker build'){
            steps {
                sh "docker build -t 'tomlarrow/docker-helloworld' ."
            }
        }

        
    }
}