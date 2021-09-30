// def gv

pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        // stage("init") {
        //     steps {
        //         script {
        //             gv = load "script.groovy"
        //         }
        //     }
        // }
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
                    echo "building the application..."
                    sh 'mvn package'
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
                    echo "building the docker image..."
                    withCredentials([usernamePassword(credentialsId:'docker-hub-repo',passwordVariable:'PASS',usernameVariable:'USER')]){
                        sh 'docker build -t simongport/my-repo:jma-2.0 .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push simongport/my-repo:jma-2.0'
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
                    echo "deploying the application..."
                    //gv.deployApp()
                }
            }
        }
    }   
}
