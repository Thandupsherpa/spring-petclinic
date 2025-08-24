pipeline {
    agent any   // Runs on any available Jenkins agent

    tools {
        maven 'M3'      // Must match name in Manage Jenkins → Tools
        jdk 'JDK17'     // Must match name in Manage Jenkins → Tools
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'feature/add-welcome-message',
                    url: 'https://github.com/Thandupsherpa/spring-petclinic.git'
            }
        }

        stage('Build & Package') {
            steps {
                sh 'mvn clean compile package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }

    post {
        always {
            cleanWs()   // Clean up workspace after every run
        }
    }
}
