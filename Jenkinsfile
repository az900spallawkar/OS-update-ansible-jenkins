pipeline {
 environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
         ANSIBLE_CONFIG        = 'ansible.cfg'
    }

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
            sh label: '', script: 'aws ec2 create-snapshot --volume-id vol-038ad9d9f9963432a --region eu-west-2 --description "This is my ansible-jenkins volume snapshot"'
             
              }
             }
             
         stage('update OS'){
            steps {
             sh label: '', script: 'ansible-playbook -u ubuntu --key-file /var/lib/jenkins/.ssh/jenkinskey -i inventory.inv update.yml'
           
             
            // ansiblePlaybook credentialsId: 'private_key', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'inventory.inv', playbook: 'update.yml'
            }
            }
           stage('Make sure updates done') {
            steps {
            sh label: '', script: 'ansible -i inventory.inv -a "lsb_release -a"'
             
              }
             }
        
      }
}
