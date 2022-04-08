pipeline{
    agent {label "agentfarm"}
    stages{
        stage('delete the workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Installing Ansible'){
            steps{
                script{
                    def ansible_exists = fileExists '/usr/bin/ansible'
                    if (ansible_exists == true){
                        echo "package already exists"
                }else {
                   sh 'sudo apt install -y wget tree unzip ansible python' 
                }
              
            }
        }
    }
        stage('Download Ansible Code'){
            steps{
                git credentialsId: 'git-repo-creds', url: 'git@github.com:ParulArinTech/ansible-webserver.git'
            }
        }
    }
}