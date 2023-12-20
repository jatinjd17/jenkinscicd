pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/jatinjd17/jenkinscicd.git'
        BRANCH = 'main'
        EC2_USER = 'ubuntu'
        EC2_PUBLIC_IP = '13.201.48.249'
    }

    stages {
        stage('Deploy to EC2') {
            steps {
                // SSH into the EC2 instance and run commands
                script {
                    sshCommand remote: [
                        host: EC2_PUBLIC_IP,
                        user: EC2_USER,
                        credentialsId: '1'
                    ], command: """
                        cd /app
                        git pull origin ${BRANCH}
                        npm install
                        npm run dev
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
    }
}
