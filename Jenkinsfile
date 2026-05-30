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
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {

                bat '''
                scp -o StrictHostKeyChecking=no ^
                -i C:\\Users\\User\\.ssh\\Jenkins-Testing.pem ^
                target\\Jenkins-Test-0.0.1-SNAPSHOT.jar ^
                ubuntu@3.7.252.55:/home/ubuntu/app.jar
                '''

                bat '''
                ssh -o StrictHostKeyChecking=no ^
                -i C:\\Users\\User\\.ssh\\Jenkins-Testing.pem ^
                ubuntu@3.7.252.55 ^
                "pkill -f app.jar || true"
                '''

                bat '''
                ssh -o StrictHostKeyChecking=no ^
                -i C:\\Users\\User\\.ssh\\Jenkins-Testing.pem ^
                ubuntu@3.7.252.55 ^
                "nohup java -jar /home/ubuntu/app.jar > app.log 2>&1 &"
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful'
        }

        failure {
            echo 'Deployment failed'
        }
    }
}
