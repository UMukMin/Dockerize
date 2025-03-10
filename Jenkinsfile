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
                            [$class: 'SubmoduleOption',
                            recursiveSubmodules: true,
                            ]
                        ]
                    ])
                }
            }
        }

        stage('Build') {
            steps {
                sh '''
                echo "Navigating to BackEnd directory..."
                cd $WORKSPACE
                echo "Building images..."
                docker-compose build
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                echo "Stopping old container..."
                cd $WORKSPACE
                docker-compose down

                echo "Starting new container..."
                docker-compose up -d

                '''
            }
        }
    }
}