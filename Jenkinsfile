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
                    
                        catchError (buildResult = "SUCCESS", stageResult: 'FAILURE')
                            sh "exit 1"
                            ansiColor('blue')
                            //buildResult: doesnt stop/fail the pipeline
                            //but stageResult: mark this stage as failed
                        }
                        
                    }
                }
            }
        }
    
