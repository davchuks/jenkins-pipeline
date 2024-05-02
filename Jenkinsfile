pipeline {
    agent any

    triggers {
        pollSCM('*/2 * * * *') // Check for changes every 2 minutes
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Compiling and packaging code using Maven.'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit tests with JUnit  and integration tests with Selenium .'
                    echo "Example: sh 'mvn test'"

                    echo "Running integration tests with Selenium ."
                }
            }
             post {
                success {
                    Mail subject: "Unit & Integration Tests Success - ${JOB_NAME}",
                                body: 'Unit & Integration Tests completed successfully! See build logs for details.',
                                attachLog: "${env.BUILD_LOG}",
                                to: 'davidochuks@gmail.com'
                }
                failure {
                    Mail subject: "Unit & Integration Tests Failed - ${JOB_NAME}",
                                body: 'Unit & Integration Tests failed! See build logs for details. ${BUILD_LOG}',
                                attachLog: "${env.BUILD_LOG}",
                                to: 'davidochuks@gmail.com'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Analyzing code quality with SonarQube.'
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Scanning for vulnerabilities with SAST scanner (e.g., OWASP ZAP).'
                }
            }
            post {
                success {
                    Mail subject: "Security Scan Success - ${JOB_NAME}",
                                body: 'Security scan completed successfully! See build logs for details.',
                                attachLog: "${currentBuild.rawBuild.logFilePath}",
                                to: 'davidochuks@gmail.com'
                }
                failure {
                    Mail subject: "Security Scan Failed - ${JOB_NAME}",
                                body: 'Security scan failed! See build logs for details.',
                                attachLog: "${currentBuild.rawBuild.logFilePath}",
                                to: 'davidochuks@gmail.com'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying application to staging environment using Amazon EC2 Plugin:( Manages deployments on AWS EC2 instances) '
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging environment using  VectorCAST/C++.'
                }
                post {
                    success {
                        Mail subject: "Integration Tests on Staging Success - ${JOB_NAME}",
                                    body: 'Integration Tests on Staging completed successfully! See build logs for details.',
                                    attachLog: "${env.BUILD_LOG}",
                                    to: 'davidochuks@gmail.com'
                    }
                    failure {
                        Mail subject: "Integration Tests on Staging Failed - ${JOB_NAME}",
                                    body: 'Integration Tests on Staging failed! See build logs for details. ${BUILD_LOG}',
                                    attachLog: "${env.BUILD_LOG}",
                                    to: 'davidochuks@gmail.com'
                    }
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying application to production environment AWS EC2.'
                }
            }
        }
    }
}
