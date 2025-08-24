pipeline {
    agent any   // Runs on any available Jenkins agent

    tools {
        maven 'M3'      // Name must match Maven installation in Jenkins (Manage Jenkins → Tools)
        jdk 'JDK17'     // Name must match JDK installation in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
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

        // 🚀 Optional Deployment Stage
        // stage('Deploy') {
        //     steps {
        //         echo 'Deploying application...'
        //     }
        // }
    }

    post {
        always {
            cleanWs()   // Clean up workspace after every run
        }
    }
}
