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
                            [$class: 'CloneOption', depth: 1, noTags: false, shallow: false],
                        ]
                    ])
                    sh '''
                    echo "Forcing submodules to update..."
                    git submodule deinit -f
                    git submodule update --init --recursive
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                sh '''
                echo "Navigating to BackEnd directory..."
                cd $WORKSPACE
                echo "Listing files in current directory..."
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