#!groovy

def registry = "registry.dev.yashkov.org/yashkov"

pipeline {
    agent {
        kubernetes {
            inheritFrom 'kaniko'
            defaultContainer 'kaniko'
        }
    }

    options {
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '3'))
    }

    stages {
        stage('maven') {
            environment {
                CONTEXT ="$WORKSPACE/maven"
                IMAGE = "$registry/maven"
            }

            steps {
                sh '''/kaniko/executor \
-c $CONTEXT -f $CONTEXT/Dockerfile \
--build-arg source=3.8.4-eclipse-temurin-17-alpine \
--destination=$IMAGE:3.8.4-jdk17 --destination=$IMAGE:latest'''
            }
        }
    }
}
