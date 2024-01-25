pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/Tharun20011/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t tharunselvarangam/phpprojectv1 .'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockers', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push tharunselvarangam/phpprojectv1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe21 -p 8081:80 tharunselvarangam/phpprojectv1'
                    sshagent(credentials: ['ubuntu']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe -p 8082:80 tharunselvarangam/phpprojectv1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@52.63.70.241 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
