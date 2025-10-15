pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/thinkwaytosolve/think.git', branch: 'main'
            }
        }
         stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }
        
    }
}
