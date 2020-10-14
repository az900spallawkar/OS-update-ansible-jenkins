pipeline {

 agent  any
        options {
                timestamps ()
                ansiColor('xterm')
            }
 
    stages {
    
        stage('SCM checkout') {
            steps {
            git "https://github.com/az900spallawkar/OS-update-ansible-jenkins"
            }
        }
        stage('Ansible init') {
            steps {
             script {
               def tfHome = tool name: 'Ansible'
               env.PATH = "${tfHome}:${env.PATH}"
               sh 'ansible --version'
             }
            }
        }
       
        
        stage('create snapshot for backup') {
            steps {
            sh label: '', script: 'aws ec2 create-snapshot --volume-id vol-038ad9d9f9963432a --description "This is my ansible-jenkins volume snapshot"'
              }
             }
             
         stage('update OS'){
            steps {
            sh label: '', script: 'ansible-playbook -u ubuntu --key-file /var/lib/jenkins/.ssh/jenkinskey -i inventory, update.yml'
            }
            }
        
      }
}
