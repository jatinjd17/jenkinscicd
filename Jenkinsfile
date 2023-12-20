pipeline {
    agent any

    environment {
        APPLICATION_NAME = 'jenkinscicddd'
        DEPLOYMENT_GROUP = 'j3dev'
        EC2_USER = 'ubuntu'
        EC2_PUBLIC_IP = '13.201.48.249'
    }

    stages {
      

        stage('Deploy to EC2 using CodeDeploy') {
            steps {
                // Copy files to EC2 using SSH
                script {
                    withCredentials([sshUserPrivateKey(credentialsId: '1', keyFileVariable: '/home/ubuntu/.ssh/authorized_keys')]) {
                        sh """
                            ssh -i /home/ubuntu/.ssh/authorized_keys ${EC2_USER}@${EC2_PUBLIC_IP} 'mkdir -p /app'
                            scp -i /home/ubuntu/.ssh/authorized_keys -r * ${EC2_USER}@${EC2_PUBLIC_IP}:/app/
                        """
                    }
                }
            }
        }

        stage('Restart Application') {
            steps {
                // Restart your Next.js application on the EC2 instance
                script {
                    withCredentials([sshUserPrivateKey(credentialsId: '1', keyFileVariable: '/home/ubuntu/.ssh/authorized_keys')]) {
                        sh """
                            ssh -i /home/ubuntu/.ssh/authorized_keys ${EC2_USER}@${EC2_PUBLIC_IP} 'cd /app && npm install && npm run dev'
                        """
                    }
                }
            }
        }
    }
}
