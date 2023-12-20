pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Check out the source code from the specified Git branch
                    git branch: "main", url: 'https://github.com/jatinjd17/jenkinscicd.git'
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                script {
                    // Use SSH to execute a script on the EC2 instance
                    sshagent(['1']) {
                        sh 'ssh -T -i /home/ubuntu/december2023ubuntu.pem ubuntu@ec2-13-201-48-249.ap-south-1.compute.amazonaws.com'
                        sh 'mkdir app'
                        sh 'cd /app'
                        sh 'touch file.txt'
                    }
                }
            }
        }
    }
}
