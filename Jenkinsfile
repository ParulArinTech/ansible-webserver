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
        stage('Run Ansible-lint against playbooks'){
            steps{
                sh 'docker run --rm -v $WORKSPACE/playbooks:/data cytopia/ansible-lint:4 apache-install.yml'
                sh 'docker run --rm -v $WORKSPACE/playbooks:/data cytopia/ansible-lint:4 website-update.yml'
                sh 'docker run --rm -v $WORKSPACE/playbooks:/data cytopia/ansible-lint:4 website-test.yml'
            }
            
        }
        stage('send slack notification'){
            steps{
                slackSend color: 'warning', message: "Parul: Please approve ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.JOB_URL} | Open>)"
                
            }
            
        }
        stage('request input'){
            steps{
                input 'please approve / deny this build'
            }
        }
    }
}