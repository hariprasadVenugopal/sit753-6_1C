pipeline {
    agent any
    environment {
        STAGING_ENVIRONMENT = 'AWS EC2 - Staging'
        PRODUCTION_ENVIRONMENT = 'AWS EC2 - Production'
    }
    stages {
        stage('Build') {
            steps {
                echo "fetch the source code from the directory path"
                echo "building code using Maven"
            }
        }
        stage('Unit tests and Integration tests') {
            steps {
                echo "running unit tests using JUnit"
                echo "running integration tests using Selenium"
            }
            post {
                success {
                    echo 'Unit and Integration Tests passed!'
                    emailext(
                        subject: "SUCCESS: Unit and Integration Tests",
                        body: "The unit and integration tests passed successfully.",
                        to: 'developer@example.com'
                    )
                }
                failure {
                    echo 'Unit and Integration Tests failed!'
                    emailext(
                        subject: "FAILURE: Unit and Integration Tests",
                        body: "The unit and integration tests failed. Please check the logs.",
                        to: 'developer@example.com'
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo "analysing the code using SonarQube"
            }
        }
        stage(' Security Scan') {
            steps {
                echo "performing security scan using OWASP ZAP"
            }
            post {
                success {
                    echo 'Security Scan passed!'
                    emailext(
                        subject: "SUCCESS: Security Scan",
                        body: "The security scan passed successfully.",
                        to: 'jnknstester@gmail.com'
                    )
                }
                failure {
                    echo 'Security Scan failed!'
                    emailext(
                        subject: "FAILURE: Security Scan",
                        body: "The security scan has found issues. Please review the security report.",
                        to: 'jnknstester@gmail.com'
                    )
                }
            }
        }
        stage('Deploying to Staging') {
            steps {
                echo "deploying  the application to the staging server: ${env.STAGING_ENVIRONMENT}"
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "running unit tests using JUnit"
                echo "running integration tests using Selenium"
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "deploying to production environment: ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
    }
}

