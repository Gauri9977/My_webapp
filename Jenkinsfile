pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Check out the code from the GitHub repository
                git branch: 'main', url: 'https://github.com/Gauri9977/My_webapp.git'
            }
        }
        
        stage('Build Maven Project') {
            steps {
                // Clean and build the Maven project
                script {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Deploy the .war file to the Tomcat server
                script {
                    deploy adapters: [tomcat9(credentialsId: 'tomcat-cred', path: '', url: 'http://localhost:8080')],
                    war: '**/*.war'
                }
            }
        }
    }

    post {
        always {
            // Post actions such as archiving artifacts or sending notifications
            archiveArtifacts artifacts: '**/target/*.war', allowEmptyArchive: true
        }
    }
}
