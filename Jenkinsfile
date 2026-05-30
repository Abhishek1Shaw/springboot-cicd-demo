pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {

                sshagent(['aws-ec2-key']) {

                    bat '''
                    scp target\\*.jar ubuntu@3.7.252.55:/home/ubuntu/app.jar
                    '''

                    bat '''
                    ssh ubuntu@3.7.252.55 "pkill -f app.jar || true"
                    '''

                    bat '''
                    ssh ubuntu@3.7.252.55 "nohup java -jar /home/ubuntu/app.jar > app.log 2>&1 &"
                    '''
                }
            }
        }
    }
}