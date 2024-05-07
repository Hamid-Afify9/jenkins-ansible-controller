//use try and catch to mark a stage as unstable in the third stage test, build, deploy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                        echo 'Testing..'
                    }
                }
            
        
        stage('Deploy') {
            steps {
                script {
                    try {
                        echo 'Deploying....'
                    } catch (Exception e) {
                        currentBuild.result = 'UNSTABLE'
                        throw e
                    }
                }
            }
        }
    }
}