#!/user/bin/env groovy

library identifier: 'jenkins-shared-library@main', retriever: modernSCM(
    [$class: 'GitSCMSource',
     remote: 'https://github.com/Sy-Tech23/jenkins-shared-library',
     credentialsId: "sy-tech23"
    ]
)


def gv

pipeline {
    agent any
    tools {
        maven 'maven'
    }
    environment {
        IMAGE_NAME = 'shersi32/myapp:1'
    }



    stages {

        stage("build app") {
           
            steps {
                script {
                    echo 'Building application jar..'
                    buildJar()
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo 'Building docker image'
                  buildImage(env.IMAGE_NAME)
                  dockerLogin()
                  dockerPush(env.IMAGE_NAME)
                    }
                }
            }
        stage("deploy") {
            
            steps {
                script {
                    echo 'Deploying docker image to EC2'
                    def dockerCmd = "docker run -p 8080:8080 -d ${IMAGE_NAME}"
                sshagent(['ec2-server']) {
                  sh "ssh -o StrictHostKeyChecking=no ec2-user@54.175.82.44 ${dockerCmd}"
                    }
                }
            }
        }
    }   
}
