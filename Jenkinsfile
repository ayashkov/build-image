#!groovy

def alpineVersion = '3.15.0'
def npmVersion = '8.1.3'
def nodeVersion = '16.13.2'
def nodeLevel = '0'
def angularVersion = '13.1.0'
def angularLevel = '0'
def mavenVersion = '3.8.3'
def mavenLevel = '0'
def registry = 'registry.dev.yashkov.org/yashkov'

def nodeImage = "${registry}/node"
def angularImage = "${registry}/angular"
def mavenImage = "${registry}/maven"

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
--destination=${nodeImage}:${nodeVersion}.${nodeLevel} \
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
--build-arg source=${nodeImage}:${nodeVersion}.${nodeLevel} \
--build-arg angular_version=${angularVersion} \
--destination=${angularImage}:${angularVersion}.${angularLevel} \
--destination=${angularImage}:latest"""
            }
        }

        stage('maven') {
            environment {
                CONTEXT ="$WORKSPACE/maven"
            }

            steps {
                sh """\
/kaniko/executor -c $CONTEXT -f $CONTEXT/Dockerfile \
--build-arg source=${angularImage}:${angularVersion}.${angularLevel} \
--build-arg maven_version=${mavenVersion} \
--destination=${mavenImage}:${mavenVersion}.${mavenLevel} \
--destination=${mavenImage}:latest"""
            }
        }
    }
}
