pipeline {
    agent any   // Can refine with label: e.g., agent { label 'maven-node' }
    
    tools {
        maven 'M3'      // Use the Maven installation configured in Jenkins (Manage Jenkins > Global Tool Config)
        jdk 'JDK17'     // Use the JDK installation configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout from your fork (replace with your username)
                git branch: "${main}", 
                    url: "https://github.com/Thandupsherpa/spring-petclinic.git"
            }
        }

        stage('Build & Package') {
            steps {
                // Compile and package into a JAR
                sh 'mvn clean compile package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                // Run tests
                sh 'mvn test'
            }
            post {
                always {
                    // Publish JUnit test results even if stage fails
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        // 🚀 You could add a Deploy stage here later
        // stage('Deploy to Staging') { ... }
    }

    post {
        always {
            // Clean up workspace after every run
            cleanWs()
        }
    }
}
