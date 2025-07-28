pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'cursodvops/jenkinsexample'
    }

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Dago-H/RepoDemo3.git'
            }
        }

        //stage('Build') {
        //    steps {
        //        bat 'echo "Probando ......"'
        //    }
        //}

        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentia') {
                        dockerImage.push('latest')
                    }
                }
            }
            post {
                success {
                    bat 'echo "Docker image pushed successfully! exito ....."'
                }
                failure {
                    bat 'echo "Failed to push Docker image. Fallo ....."'
                }
            }
        }

    }
}