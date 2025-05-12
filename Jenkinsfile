pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                script {
                    try {
                        echo 'Running tests...'
                        // simulate test command
                        sh 'echo "test log" > test.log'
                    } catch (err) {
                        currentBuild.result = 'FAILURE'
                        throw err
                    }
                }
            }
            post {
                always {
                    emailext (
                        subject: "Test Stage: ${currentBuild.currentResult}",
                        body: "The test stage has ${currentBuild.currentResult}. See attached logs.",
                        to: "uthpalagamage166@gmail.com",
                        attachmentsPattern: 'test.log'
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    try {
                        echo 'Running security scan...'
                        sh 'echo "security scan log" > scan.log'
                    } catch (err) {
                        currentBuild.result = 'FAILURE'
                        throw err
                    }
                }
            }
            post {
                always {
                    emailext (
                        subject: "Security Scan: ${currentBuild.currentResult}",
                        body: "The security scan has ${currentBuild.currentResult}. Logs are attached.",
                        to: "uthpalagamage166@gmail.com",
                        attachmentsPattern: 'scan.log'
                    )
                }
            }
        }
    }
}
