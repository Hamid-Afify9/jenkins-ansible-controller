pipeline {
    agent any

    stages {
        stage('print hello'){
            steps {
                echo 'Hello World'
                sh 'ansible-playbook -i hosts ansible-controller.yaml -u ubuntu '
            }
        }

        stage('copying ansible files to ansible-controller') {
            steps {
                echo 'Copying files to ansible-controller'
                sshagent (credentials: ['jenkins-ssh']) {
                    sh 'scp -o StrictHostKeyChecking=no ansible/*  ubuntu@ip:/root/hello.txt '
                    withCredentials([sshUserPrivateKey(credentialsId: 'id-here', keyFileVariable: 'keyfile', usernameVariable: 'user' )])
                    {
                        sh 'scp ${keyfile}  ubuntu@ip:root/ssh-key.pem '
                    }
            }


            }
            // first install this plugin 'SSH Pipeline Steps'
            // stage('run the play-book on ansible-controller') {
            //     steps {
            //         echo 'Running the playbook on ansible-controller'
            //         def remote = [:]
            //         remote.name = 'ansible-controller'
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
