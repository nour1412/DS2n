pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME' // Le nom que tu as bien configuré
        jdk 'JDK17'         // Ton JDK déclaré
    }

    environment {
        SONAR_PROJECT_KEY = 'DS2n'
    }

    stages {
        stage('Clone Project') {
            steps {
                git 'https://github.com/nour1412/DS2n.git'
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                 withSonarQubeEnv('SonarQubeServer') {
      bat "mvn sonar:sonar -Dsonar.projectKey=DS2n -Dsonar.token=squ_8c84ed6357dda7fd8216a891ed9aebf596cacec8"

                }
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t studentdashboard:latest .'
            }
        }
    }
}
