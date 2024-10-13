pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Install Node.js and npm') {
            steps {
                script {
                    // Install Node.js and npm if they are not already installed
                    sh '''
                    if ! command -v node &> /dev/null; then
                        echo "Node.js is not installed. Installing..."
                        curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
                        sudo apt-get install -y nodejs
                    else
                        echo "Node.js is already installed."
                    fi

                    if ! command -v npm &> /dev/null; then
                        echo "npm is not installed. Installing..."
                        sudo apt-get install -y npm
                    else
                        echo "npm is already installed."
                    fi
                    '''
                }
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
    }
}
