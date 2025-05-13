pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME' // Déclaré dans Jenkins
        jdk 'JDK17'         // Déclaré dans Jenkins
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
