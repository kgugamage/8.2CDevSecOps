pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
        SONAR_TOKEN = credentials('SONAR_TOKEN') // Jenkins will inject your SonarCloud token here
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/kgugamage/8.2CDevSecOps.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }

<<<<<<< HEAD
        stage('NPM Audit') {
            steps {
                sh 'npm audit --audit-level=high || true'
=======
        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit') {
            steps {
                sh 'npm audit || true'
>>>>>>> 70c2e70df49f9a8a9a4a45c9fb6798aec1d3e64c
            }
        }

        stage('SonarCloud Analysis') {
            steps {
<<<<<<< HEAD
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    sh '''
                        curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006.zip
                        unzip -q sonar-scanner.zip
                        ./sonar-scanner-*/bin/sonar-scanner
                    '''
                }
=======
                sh '''
                curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip
                unzip sonar-scanner.zip
                export PATH=$PATH:$(pwd)/sonar-scanner-*/bin
                sonar-scanner
                '''
>>>>>>> 70c2e70df49f9a8a9a4a45c9fb6798aec1d3e64c
            }
        }
    }
}
