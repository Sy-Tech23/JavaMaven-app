#!/user/bin/env groovy

@Library ('jenkins-shared-library')
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
        
           
            steps {
                script {
                  buildImage 'shersi32/my-repo:jma-3.0'
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
