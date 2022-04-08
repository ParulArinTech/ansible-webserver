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
              sh 'sudo apt install wget tree unzip ansible python'
            }
        }
        stage('third stage'){
            steps{
                echo "third stage"
            }
        }
    }
}