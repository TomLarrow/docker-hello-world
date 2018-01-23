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

        stage ('check image'){
            agent {
                docker {
                    image 'tomlarrow/docker-helloworld'
                }
            }
            steps{
                echo "Look ma I'm inside the container"
                sh "cat /www/index.html"
                sh "cat /www/index.html|grep 'Hello Worlb'"
            }
        }
    }

    post {
        success {
            echo "Pipeline was successful"
        }
        failure{
            echo "Pipeline encountered an error"
        }
        always{
            echo "This always happens"
        }
    }
}