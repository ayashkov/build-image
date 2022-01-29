#!groovy

def alpineVersion = '3.15.0'
def jreVersion = '17.0.2'
def jreLevel = '0'
def nodeVersion = '16.13.2'
def nodeLevel = '1'
def npmVersion = '8.1.3'
def npmLevel = '0'
def angularVersion = '13.1.0'
def angularLevel = '1'
def mavenVersion = '3.8.3'
def mavenLevel = '2'
def registry = 'registry.dev.yashkov.org/yashkov'

def jreImage = "${registry}/jre"
def nodeImage = "${registry}/node"
def npmImage = "${registry}/npm"
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
        stage('jre') {
            environment {
                CONTEXT ="$WORKSPACE/jre"
            }

            steps {
                sh """\
/kaniko/executor -c $CONTEXT -f $CONTEXT/Dockerfile \
--use-new-run \
--build-arg source=alpine:${alpineVersion} \
--build-arg jre_version=${jreVersion} \
--destination=${jreImage}:${jreVersion}.${jreLevel} \
--destination=${jreImage}:latest"""
            }
        }

        stage('node') {
            environment {
                CONTEXT ="$WORKSPACE/node"
            }

            steps {
                sh """\
/kaniko/executor -c $CONTEXT -f $CONTEXT/Dockerfile \
--use-new-run \
--build-arg source=alpine:${alpineVersion} \
--build-arg node_version=${nodeVersion} \
--destination=${nodeImage}:${nodeVersion}.${nodeLevel} \
--destination=${nodeImage}:latest"""
            }
        }

        stage('npm') {
            environment {
                CONTEXT ="$WORKSPACE/npm"
            }

            steps {
                sh """\
/kaniko/executor -c $CONTEXT -f $CONTEXT/Dockerfile \
--use-new-run \
--build-arg source=${nodeImage}:${nodeVersion}.${nodeLevel} \
--build-arg npm_version=${npmVersion} \
--destination=${npmImage}:${npmVersion}.${npmLevel} \
--destination=${npmImage}:latest"""
            }
        }

        stage('angular') {
            environment {
                CONTEXT ="$WORKSPACE/angular"
            }

            steps {
                sh """\
/kaniko/executor -c $CONTEXT -f $CONTEXT/Dockerfile \
--use-new-run \
--build-arg source=${npmImage}:${npmVersion}.${npmLevel} \
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
--use-new-run \
--build-arg source=${npmImage}:${npmVersion}.${npmLevel} \
--build-arg maven_version=${mavenVersion} \
--destination=${mavenImage}:${mavenVersion}.${mavenLevel} \
--destination=${mavenImage}:latest"""
            }
        }
    }
}
