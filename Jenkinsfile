pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/nithinraghu1997/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t nithu12678/3febimg:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push nithu12678/3febimg:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe21 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe21 -p 8082:80 nithu12678/3febimg:v1'
                    sshagent(['ssh-cred']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe211 -p 8082:80 akshu20791/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@3.91.61.233 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@54.211.82.97 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
