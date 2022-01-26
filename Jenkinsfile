#!groovy

def alpineVersion = '3.15.0'
def nodeVersion = '16.13.2'
def npmVersion = '8.1.3'
def angularVersion = '13.1.0'
def registry = 'registry.dev.yashkov.org/yashkov'

def nodeImage = "${registry}/node"
def angularImage = "${registry}/angular"

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
        stage('node') {
            environment {
                CONTEXT ="$WORKSPACE/node"
            }

            steps {
                sh """\
/kaniko/executor -c $CONTEXT -f $CONTEXT/Dockerfile \
--build-arg source=alpine:${alpineVersion} \
--build-arg node_version=${nodeVersion} \
--build-arg npm_version=${npmVersion} \
--destination=${nodeImage}:${nodeVersion} \
--destination=${nodeImage}:latest"""
            }
        }

        stage('angular') {
            environment {
                CONTEXT ="$WORKSPACE/angular"
            }

            steps {
                sh """\
/kaniko/executor -c $CONTEXT -f $CONTEXT/Dockerfile \
--build-arg source=${nodeImage}:${nodeVersion} \
--build-arg angular_version=${angularVersion} \
--destination=${angularImage}:${angularVersion} \
--destination=${angularImage}:latest"""
            }
        }
    }
}
