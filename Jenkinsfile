#!/user/bin/env groovy
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
         stage("test") {
            steps {
                script {
                     echo "testing the application..."
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
                     gv.buildJar()
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
                   gv.buildImage()
                    }
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
