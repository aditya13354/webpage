pipeline {
    agent any
    environment {
        registry = '551584873343.dkr.ecr.us-east-1.amazonaws.com/demo:latest'
    }
    stages {
        stage("Checkout") {
             stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
            }
        }
        stage("Docker Build") {
            steps {
                sh "docker build -t demo:latest ."
            }
        }
        stage("ECR Login") {
            steps {
                withAWS(credentials:'aws-credential') {
                    script {
                        def login = ecrLogin()
                        sh "${login}"
                    }
                }
            }
        }
        stage("Docker Push") {
            steps {
                sh "docker push ${registry}"
            }
        }
    }
    post {
        success {
            echo 'ending'
        }
    }
}
