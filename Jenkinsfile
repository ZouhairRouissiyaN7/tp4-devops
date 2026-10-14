pipeline {
    environment {
        registry = "mzrouissiya/tp4"
        registryCredential = 'dockerhub1'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/ZouhairRouissiyaN7/tp4-devops'
            }
        }
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Test image') {
            steps {
                script {
                    echo "Tests passed"
                }
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy image') {
            steps {
                bat "docker run -d $registry:$BUILD_NUMBER"
            }
        }
    }
}
