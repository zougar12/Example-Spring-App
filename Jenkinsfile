pipeline {
    agent none

    environment {
        DOCKER_HUB_USERNAME = credentials('DOCKER_HUB_USERNAME')
        DOCKER_HUB_PASSWORD = credentials('DOCKER_HUB_TOKEN')
        CURRENT_COMMIT = getCommitHash()
    }

    stages {
        stage('Unit tests') {
            agent {
                docker {
                    image 'openjdk:17'
                    args '-v $HOME/.m2:/root/.m2'
                }
            }
            steps {
                sh 'chmod u+x ./mvnw'
                sh './mvnw test'
            }
        }
    }
}

def getCommitHash() {
    node {
        return sh(script: 'git rev-parse --short HEAD', returnStdout: true)
    }
}