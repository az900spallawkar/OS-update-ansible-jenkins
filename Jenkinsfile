pipeline {

 agent  any
        options {
                timestamps ()
                ansiColor('xterm')
            }
 
    stages {
    
        stage('SCM checkout')
            steps {
            git "https:/https://github.com/az900spallawkar/OS-update-ansible-jenkins"
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
            sh "aws ec2 create-snapshot --volume-id vol-059f47f3d630dcdaa --description "This is my root volume snapshot""
              }
             }
             
        stage('update OS')
            steps {
            sh "ansible-playbook -u ubuntu --key-file /var/lib/jenkins/.ssh/jenkinskey -i inventory, main.yml"

            }
        
      }
}
