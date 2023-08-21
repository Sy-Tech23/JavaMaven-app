#!/user/bin/env groovy

pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
         stage("test") {
            steps {
                script {
                     echo "testing the application..."
                     echo "executing test for branch $BRANCH_NAME"
                }
            }
        }
        stage("build ") {
           
            steps {
                script {
                  echo "building the application."
                }
            }
        }
    
        stage("deploy") {
            
            steps {
                script {
                    echo 'Deploying docker image to EC2'
                    def dockerCmd = "docker run -p 3080:3080 -d shersi32/myapp:1 "
                sshagent(['ec2-server-key']) {
                  sh "ssh -o StrictHostKeyChecking=no ec2-user@54.175.82.44 ${dockerCmd}"
                    }
                }
            }
        }
    }   
}
