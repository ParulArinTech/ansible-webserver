pipeline{
    agent any
    stages{
        stage('delete the workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Second stage'){
            steps{
                echo "second stage"
            }
        }
        stage('third stage'){
            steps{
                echo "third stage"
            }
        }
    }
}