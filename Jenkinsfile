#!/user/bin/env groovy

@library ('jenkins-shared-library')
def gv

pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
         stage("test") {
            steps {
                script {
                     echo "testing the application..."
                     echo "executing test for branch $BRANCH_NAME"
                }
            }
        }
        stage("build jar") {
            when{
                expression{
                BRANCH_NAME=='main'
                }
            }
            steps {
                script {
                    buildJar()
                }
            }
        }
        stage("build image") {
            when{
                expression{
                BRANCH_NAME=='main'
                }
            }
            steps {
                script {
                  buildImage()
                    }
                }
            }
        stage("deploy") {
            when{
                expression{
                BRANCH_NAME=='main'
                }
            }
            steps {
                script {
                    gv.deployApp()
                    }
                }
            }
        }
    }   
