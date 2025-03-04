pipeline {
    agent {
        docker {
            image 'postman/newman'  
            args '--entrypoint=""'
        }
    }
    
    options([
        parameters([
            string(name: 'COLLECTION_NAME', defaultValue: 'SimpleGroceryStoreAPI.postman_collection', description: 'Nom de la collection Postman à exécuter')
        ])
    ])

    stages {
        stage('Check Newman version') {
            steps {
                sh 'newman --version'
            }
        }

        stage('Run collection test') {
            steps {
                script {
                    sh "newman run collections/${COLLECTION_NAME} -r cli,junit,html --reporter-html-export=newman-report.html --reporter-junit-export=newman-report.xml"
                }
            }
        }

        stage('Check Generated Files') {
            steps {
                script {
                    sh 'ls -l'
                    sh 'if [ -f newman-report.html ]; then echo "✅ newman-report.html found!"; else echo "❌ newman-report.html NOT found!"; fi'
                }
            }
        }
    }

    post {
        always {
            junit 'newman-report.xml'
            archiveArtifacts artifacts: 'newman-report.html', allowEmptyArchive: true
        }
    }
}
