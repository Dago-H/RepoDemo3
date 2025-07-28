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

stage('Build') {
    steps {
        bat 'echo "Building the application"'
    }
}

        stage('Test') {
            steps {
                bat 'echo "Running tests"'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Deploy') {
            steps {
                bat 'echo "Ejemplo"'
            }
        }   


}