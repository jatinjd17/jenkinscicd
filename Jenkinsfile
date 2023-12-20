pipeline {
    agent any

    environment {
        APPLICATION_NAME = 'jenkinscicdpipelineee'
        DEPLOYMENT_GROUP = 'devvv'
        EC2_USER = 'ubuntu'
        EC2_PUBLIC_IP = '13.201.48.249'
    }

    stages {


        stage('Deploy to EC2 using CodeDeploy') {
            steps {
                // Copy files to EC2 using SSH
                script {
                    sshCommand remote: [
                        host: '13.201.48.249',
                        user: 'ubuntu',
                        credentialsId: '1'
                    ], command: """
                        mkdir -p /app
                        cd /app
                        rm -rf *
                    """
                    sh "cp -r * ubuntu@13.201.48.249:/app/"
                }
            }
        }

        stage('Restart Application') {
            steps {
                // Restart your Next.js application on the EC2 instance
                script {
                    sshCommand remote: [
                        host: '13.201.48.249',
                        user: 'ubuntu',
                        credentialsId: '1'
                    ], command: """
                        cd /app
                        npm install
                        npm run dev
                    """
                }
            }
        }
    }
}
