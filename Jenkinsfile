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
        stage('Run collection test'){
            steps{
                sh 'newman run collections/SimpleGroceryStoreAPI.postman_collection'
            }
        }
    }
}