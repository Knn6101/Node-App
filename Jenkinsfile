pipeline{
    agent any

    environment{
        EC2_HOST = ""
        SSH_CREDENTIAL_ID = ""
        REMOTE_USER = "ubuntu"
        REMOTE_PATH = "/home/ubuntu/app"
        WEB_ROOT = "/var/www/html"
        SERVER = "nginx"
    }

    stages{
        stage("Build"){
            steps{
                echo "Installing Dependencies"
                sh "npm install"
                echo "Building the app"
                sh "npm run build"
                echo "Build complete"
            }
        }
        stage("Deploy"){
            steps{
                echo "Starting Deployment"
                sshagent(credential: [env.SSH_CREDENTIAL_ID]){
                    sh"""
                       echo "Creating Remote Directory"
                       ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${EC2_HOST} 'mkdir-p ${REMOTE_PATH}'

                       echo "Copying Distribution to Remote Path"
                       scp -o StrictHostKeyChecking=no -r dist/* ${REMOTE_USER}@${EC2_HOST}:${REMOTE_PATH}/

                       echo "Rstarting Nginx"
                       ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${EC2_HOST}'
                            sudo rm-rf ${WEB_ROOT}/*
                            sudo cp -r ${REMOTE_PATH}/* ${WEB_ROOT}/
                            sudosystemctl restart ${SERVER} 
                       '
                    """
                }
            }
        }

    }
}