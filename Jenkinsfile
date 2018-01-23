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
                sh "cat /www/index.html|grep 'Hello World'"
            }
        }

        stage ('deploy image'){
            steps{
                sh "docker stop 'hello-world' || echo 'container not running'"
                sh "docker rm 'hello-world' || echo 'image does not exist'"
                sh "docker run -d --name 'hello world' -p 8675:8000 tomlarrow/docker-helloworld"
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