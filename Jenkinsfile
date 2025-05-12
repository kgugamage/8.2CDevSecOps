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
                        sh 'mkdir -p logs && echo "test log content" > logs/test.log'
                    } catch (err) {
                        currentBuild.result = 'FAILURE'
                        throw err
                    }
                }
            }
            post {
                always {
                    script {
                        try {
                            emailext(
                                subject: "Jenkins: Test Stage - ${currentBuild.result}",
                                body: "The Test stage has finished with status: ${currentBuild.result}. Please see the attached log.",
                                to: "uthpalagamage166@gmail.com",
                                attachmentsPattern: 'logs/test.log'
                            )
                        } catch (e) {
                            echo "Failed to send test stage email: ${e}"
                        }
                    }
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    try {
                        sh 'mkdir -p logs && echo "security scan log content" > logs/scan.log'
                    } catch (err) {
                        currentBuild.result = 'FAILURE'
                        throw err
                    }
                }
            }
            post {
                always {
                    script {
                        try {
                            emailext(
                                subject: "Jenkins: Security Scan Stage - ${currentBuild.result}",
                                body: "The Security Scan stage has finished with status: ${currentBuild.result}. Please see the attached log.",
                                to: "uthpalagamage166@gmail.com",
                                attachmentsPattern: 'logs/scan.log'
                            )
                        } catch (e) {
                            echo "Failed to send security scan email: ${e}"
                        }
                    }
                }
            }
        }
    }
}
