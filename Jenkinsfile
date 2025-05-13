pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9' // Déclaré dans Jenkins
        jdk 'jdk-17'         // Déclaré dans Jenkins
    }

    environment {
        SONAR_PROJECT_KEY = 'DS2n' // Change si nécessaire
    }

    stages {
        stage('Clone Project') {
            steps {
                git 'https://github.com/nour1412/DS2n.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQubeServer') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=$SONAR_PROJECT_KEY'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t studentdashboard:latest .'
            }
        }
    }
}
