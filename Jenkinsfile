pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/hamzaouakrim123/tp-jenkins.git'

            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt --break-system-packages'
            }
        }

        stage('Run Tests') {
            steps {
                sh '/var/jenkins_home/.local/bin/pytest --tb=short'
            }
        }

        stage('SCA Scan') {
            steps {
              
                sh '/opt/dependency-check/bin/dependency-check.sh --project "TP-Jenkins" --scan . --format HTML --failOnCVSS 7'

            }
        }
    }

    post {
        failure {
            echo 'Build echoue : vulnerabilites critiques detectees !'
        }
        success {
            echo 'Pipeline OK !'
        }
    }
}