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
        
        stage('create snapshot for backup') {
            steps {
            sh "aws ec2 create-snapshot --volume-id vol-059f47f3d630dcdaa --description "This is my root volume snapshot""
              }
             }
             
        stage('update OS')
            steps {
            sh "ansible-playbook -i inventory --private-key packer_saziya.pem -u ubuntu main.yml"
            }
        
      }
}
