pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
     environment {
            CI = 'true'
        }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build docker image') {
            steps {
                echo 'docker build -t pas_a/node-react-app:$(git describe --tags --abbrev=0) .'
            }
        }
        stage('Test') {
                    steps {
                        sh './jenkins/scripts/test.sh'
                    }
                }
                stage('Deliver') {
                            steps {
                                sh './jenkins/scripts/deliver.sh'
                                input message: 'Termino de usar el sitio? (Click para continuar)'
                                sh './jenkins/scripts/kill.sh'
                            }
                        }
        stage('Deployment') {
            steps {
                echo 'kubectl apply -f app-cd.yaml'
            }
        }

    }
}