pipeline {
    agent any
    environment {
        ansible_controller = "54.204.24.103"
    }

    stages {
        stage('print hello'){
            steps {
                sshagent (credentials: ['ansible-server']) {
                echo 'Hello World'
                sh 'ansible-playbook -i hosts ansible-controller.yaml -u ubuntu '}
            }
        }

        stage('copying ansible files to ansible-controller') {
            steps {
                echo 'Copying files to ansible-controller'
                sshagent (credentials: ['ansible-server']) {
                    sh 'scp -o StrictHostKeyChecking=no ansible/*  ubuntu@${ansible_controller}:/root/ '
                    withCredentials([sshUserPrivateKey(credentialsId: 'ansible-server', keyFileVariable: 'keyfile', usernameVariable: 'ubuntu' )])
                    {
                        sh 'scp ${keyfile}  ubuntu@$ansible_controller:root/ssh-key.pem '
                    }
            }


            }
            // first install this plugin 'SSH Pipeline Steps'
            // stage('run the play-book on ansible-controller') {
            //     steps {
            //         echo 'Running the playbook on ansible-controller'
            //         def remote = [:]
            //         remote.name = 'ansible_controller'
            //         remote.host = 'ip'
            //         //remote.user = 'root'
            //        //remote.password = 'password'
            //         remote.allowAnyHosts = true
            //             withCredentials([sshUserPrivateKey(credentialsId: 'id-here', keyFileVariable: 'keyfile', usernameVariable: 'user' )])
            //             {
            //             remote.identityFile = keyfile
            //             remote.user= user
            //             sshCommand remote: remote, command: 'ansible-playbook /root/hello.txt -i /root/hosts -u ubuntu '

            //             }
            //     }
            // }
        }
    }
}
