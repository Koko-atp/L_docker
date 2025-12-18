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
        
                    if [ "$(docker ps -aq -f name=^/67023042$)" ]; then
                        echo "Found container '67023042'. Restarting..."
                        docker restart 67023042
                    else
                        echo "Container '67023042' not found."
                        docker run --rm -p 5643:3000 --name 67023042 -d kokoatp/tesgitaction:main
                    fi
                    '''
                }
            }
        }
    }
}
