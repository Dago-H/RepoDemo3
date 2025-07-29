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
                    //bat 'echo "Failed to push Docker image. Fallo ....."'
                    mail to: 'trabajo.2024.comun@gmail.com',
                        from: 'trabajo.2024.comun@gmail.com',
                        subject: "Fallo al subir la imagen de Docker ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "Ha fallado la subida de la imagen de Docker al repositorio. Por favor, revisa el pipeline. ${env.JOB_NAME} #${env.BUILD_NUMBER} ${env.BUILD_URL}"
                }
            }
        }

    }
}