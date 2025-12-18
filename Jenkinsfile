pipeline {
    agent any

    stages {
        stage('Pull Docker Image') {
            steps {
                echo 'Waiting for service to initialize...' 
                sleep time: 180, unit: 'SECONDS'
                script {
                    sh '''docker pull kokoatp/tesgitaction:main'''
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh '''
        
                    if [ "$(docker ps -aq -f name=^/se67$)" ]; then
                        echo "Found container 'se67'. Restarting..."
                        docker restart se67
                    else
                        echo "Container 'se67' not found."
                        docker run --rm -p 5643:3000 --name 67023042 -d kokoatp/tesgitaction:main
                    fi
                    '''
                }
            }
        }
    }
}