pipeline {
    agent any

    environment {
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

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit') {
            steps {
                sh 'npm audit --audit-level=high || true'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    sh '''
                        # Download sonar-scanner
                        curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip

                        # Unzip sonar-scanner
                        unzip -q sonar-scanner.zip

                        # Add the sonar-scanner binary directory to PATH
                        export PATH=$PATH:$(pwd)/sonar-scanner-*/bin

                        # Run sonar-scanner
                        sonar-scanner
                    '''
                }
            }
        }
    }
}
