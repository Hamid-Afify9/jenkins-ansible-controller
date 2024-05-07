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
            
        // mark this as red flag in jenkins
        stage('Deploy') {
            steps {
                script {
                    try {
                        echo 'Deploying....'
                    } catch (Exception e) {
                        currentBuild.result = 'UNSTABLE'
                        throw e
                        catchError (buildResult = currentBuild.result, stageResult: 'FAILURE')
                            sh "exit 1"
                        }
                        
                    }
                }
            }
        }
    }
}