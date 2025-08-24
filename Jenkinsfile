pipeline {
    agent any   // This can be refined to use a label with Maven installed

    tools {
        maven 'M3'      // Tells Jenkins to use a pre-configured Maven installation
        jdk 'JDK17'     // Tells Jenkins to use a pre-configured JDK installation
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the branch that triggered the build
                git branch: "${main}", 
                    url: 'https://github.com/Thandupsherpa/spring-petclinic.git'
            }
        }

        stage('Build & Package') {
            steps {
                // Compile the code and package it into a JAR file
                sh 'mvn clean compile package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                // Run the unit tests
                sh 'mvn test'
            }
            post {
                always {
                    // Always publish the JUnit test results, even if the stage fails
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        // You can add a Deploy stage here, e.g., stage('Deploy to Staging') { ... }
    }

    post {
        always {
            // Clean up after the build
            cleanWs()
        }
    }
}
