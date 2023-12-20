pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    git 'https://github.com/jatinjd17/jenkinscicd.git'
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                script {
                    // Use SSH to execute a script on the EC2 instance
                    sshagent(['1']) {
                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.201.48.249 "bash -s" < deploy-script.sh'
                    }
                }
            }
        }
    }
}
