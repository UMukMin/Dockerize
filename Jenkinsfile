pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    echo "Cloning repository including submodules..."
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: 'master']],
                        userRemoteConfigs: [[
                            url: 'git@github.com:UMukMin/Dockerize.git',
                            credentialsId: 'github-ssh'
                        ]],
                        extensions: [
                            [$class: 'SubmoduleOption', recursiveSubmodules: true, parentCredentials: true],
                        ]
                    ])
                    sh '''
                    echo "Initializing submodules..."
                    git submodule init 
                    git submodule update --init --recursive
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                sh '''
                cd $WORKSPACE
                docker-compose build
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                echo "Restarting containers..."
                docker-compose down && docker-compose up -d
                '''
            }
        }
    }
}