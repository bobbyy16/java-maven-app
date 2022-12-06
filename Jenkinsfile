#!/usr/bin/env groovy

library identifier : 'jenkins-shared-library@main', retriever: modernSCM (
    [$class: 'GitSCMSource',
     remote: 'https://github.com/bobbyy16/jenkins-shared-library.git',
     credentials: 'github-credentials'
    ]
)
def gv

pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    buildImage 'bobbyy16/java-maven-app:2.0'
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    buildJar()
                }
            }
        }
        stage("dockerlogin") {
            steps {
                script {
                    dockerLogin()
                }
            }
        }
        stage("dockerPush") {
            steps {
                script {
                    dockerPush()
                }
            }
        }
    }
}
