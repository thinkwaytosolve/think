pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }

    triggers {
        cron('0 9 * * 1') // Every Monday at 9:00 AM IST
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'feature/meghna',
                    url: 'https://github.com/expertszen/java-standalone-application.git'
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }
        stage('Run Application') {
            steps {
                bat 'java -cp target/java-standalone-application-1.0-SNAPSHOT.jar com.expertszen.App'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Post Build Notification') {
            steps {
                emailext (
                    subject: "Jenkins Build: ${currentBuild.currentResult}",
                    body: "Build completed with status: ${currentBuild.currentResult}\nCheck console output at ${env.BUILD_URL}",
                    to: 'your-email@example.com'
                )
            }
        }
    }
}
