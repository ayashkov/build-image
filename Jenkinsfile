#!groovy

def regitry = "registry.dev.yashkov.org/yashkov"

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
                sh '''VERSION=3.8.4 /kaniko/executor \
-c $CONTEXT -f $CONTEXT/Dockerfile \
--build-arg java_version=17 --build-arg maven_version=$VERSION \
--destination=$IMAGE:$VERSION --destination=$IMAGE:latest'''
            }
        }
    }
}
