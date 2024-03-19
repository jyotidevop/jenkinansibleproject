pipeline {
    agent any 
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/jyotidevop/jenkinansibleproject.git", branch: "main"
            }
        }
        stage("copy ansible playbook and docker file to ansible server"){
            steps {
              sshagent(['ansible_demo']) {
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.80.242'
                sh 'scp /var/lib/jenkins/workspace/agent/* ubuntu@172.31.80.242:/home/ubuntu/'
            }
           }
        }
        stage("run ansible playbook to deploy container on remote server"){
            steps {
              sshagent(['ansible_demo']) {
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.80.242 cd /home/ubuntu/'
                 sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.80.242 ansible-playbook ansible.yaml'
            }
          }
        }
    }
}
