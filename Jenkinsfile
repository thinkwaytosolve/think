pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }

    triggers {
       githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                git( 
                    branch: 'feature/meghna',
                    url: 'https://github.com/expertszen/java-standalone-application.git',
                    credentialsId: 'github-pat'
                    )
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
                script {
                    if (currentBuild.currentResult == 'SUCCESS') {
                        emailext(
                            subject: "SUCCESS: Jenkins Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
                            body: """
                                The Jenkins job '${env.JOB_NAME}' has completed successfully.

                                Build Number: ${env.BUILD_NUMBER}
                                Status: SUCCESS
                                Build URL: ${env.BUILD_URL}
                            """,
                            to: 'expertszen@gmail.com'
                        )
                    } else if (currentBuild.currentResult == 'FAILURE') {
                        emailext(
                            subject: "FAILURE: Jenkins Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
                            body: """
                                The Jenkins job '${env.JOB_NAME}' has FAILED.

                                Build Number: ${env.BUILD_NUMBER}
                                Status: FAILURE
                                Check logs here: ${env.BUILD_URL}
                            """,
                            to: 'expertszen@gmail.com'
                        )
                    }
                }
            }
        }
    }
}
