pipeline{
    agent any

    environment {
        DOCKER_IMAGE = 'cursodvops/jenkinsexample'
    }

    trigger{
        githubPush()
    }
    stages{
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
    }
}