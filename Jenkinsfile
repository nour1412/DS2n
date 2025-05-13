pipeline {
    agent any

    stages {
        stage('Clone Project') {
            steps {
                // Cloning the project from GitHub
                git 'https://github.com/YassineGarram/DS-Devops.git'
            }
        }
        stage('Build with Maven') {
            steps {
                // Compiling and building the project with Maven
                sh 'mvn clean install'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    // Analyzing code quality with SonarQube
                    sh 'mvn sonar:sonar -Dsonar.login=sqa_1f4a1496329ced4de4f8e56a287a02ade4c712e6'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                // Building the Docker image
                sh 'docker build -t studentdashboard:latest .'
            }
        }
    }
}
