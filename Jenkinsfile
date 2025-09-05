pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url: 'https://github.com/Mimoh6/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t mimoh6/akshatnewimg6july:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
withCredentials([usernamePassword(credentialsId: 'docker-hub-pwd', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
    sh "echo $DOCKER_PASS | docker login -u mimoh6 --password-stdin"
}
                    sh 'docker push mimoh6/akshatnewimg6july:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 mimoh6/akshatnewimg6july:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 akshu20791/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.25.48 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.25.48 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
