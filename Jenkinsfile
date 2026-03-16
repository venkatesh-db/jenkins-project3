pipeline {


agent any

environment {
    IMAGE_NAME = "venkatesh/jenkins-project3"
    CONTAINER_NAME = "jenkins-project3-container"
    DOCKER = "/usr/local/bin/docker"
    REPO_URL = "https://github.com/venkatesh-db/jenkins-project3.git"
}

stages {

    stage('Checkout Code') {
        steps {
            git branch: 'main', url: "$REPO_URL"
        }
    }

    stage('Check Docker') {
        steps {
            sh '$DOCKER --version'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh '$DOCKER build -t $IMAGE_NAME .'
        }
    }

    stage('Stop Old Container') {
        steps {
            sh '''
            $DOCKER stop $CONTAINER_NAME || true
            $DOCKER rm $CONTAINER_NAME || true
            '''
        }
    }

    stage('Run Container') {
        steps {
            sh '$DOCKER run -d -p 8081:8080 --name $CONTAINER_NAME $IMAGE_NAME'
        }
    }

}


}
