pipeline {
    agent any

    tools {
        maven 'Maven 3.8.1'  // Must match Maven version name configured in Jenkins
        jdk 'Java 11'        // Must match JDK name in Jenkins tools config
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/YOUR_USERNAME/maven-jenkins-demo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
