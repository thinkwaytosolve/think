
pipeline {
    agent any

    environment {
        TZ = "Asia/Kolkata"
    }

    options {
        timeout(time: 10, unit: 'MINUTES')  // Build timeout
    }

    triggers {
        cron('TZ=Asia/Kolkata\n0 3 * * 1') // Every Monday 9:00 AM IST
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/expertszen/java-standalone-application.git'
            }
        }

        stage('Build Java Program') {
            steps {
                sh 'javac HelloWorld.java'
            }
        }

        stage('Run Java Program') {
            steps {
                sh 'java HelloWorld'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully.'
        }
        failure {
            mail to: 'your-email@example.com',
                 subject: "Jenkins Job Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Check Jenkins for details: ${env.BUILD_URL}"
        }
    }
}
