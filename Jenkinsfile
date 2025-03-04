pipeline{
    agent {
        docker {
            image 'postman/newman'  
            args '--entrypoint=""'
        }
    }
    stages{
        stage('Check Newman version'){
            steps{
                sh 'newman --version'
            }
        }
    }
}