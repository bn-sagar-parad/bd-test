pipeline {
    agent any
    environment {
        POLARIS__TOKEN = credentials('POLARIS_TOKEN')
    }
 
    stages {
 
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/bn-sagar-parad/JuiceShop.git'
            }
        }
 
        stage('Build') {
            steps {
                echo 'Building GitHub project...'
            }
        }
 
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
 
        stage('Pre Scan') {
            steps {
                echo 'Running pre checks for scan...'
            }
        }
        stage('Polaris Black Duck Security Scan') {
            steps {
                security_scan(
                    product: 'polaris',
                    polaris_server_url: POLARIS_URL,
                    polaris_access_token: POLARIS__TOKEN,
                    polaris_application_name: "${env.JOB_NAME}",
                    polaris_project_name: "${env.JOB_NAME}",
                    polaris_branch_name: "${env.BRANCH_NAME}",
                    polaris_assessment_types: 'SAST,SCA'
                )
            }
        }
    }
 
    post {
        success {
            echo 'Pipeline completed successfully'
        }
 
        failure {
            echo 'Pipeline failed'
        }
    }
}
