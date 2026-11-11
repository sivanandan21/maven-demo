pipeline {

    agent {
        label 'linux-agent'
    }

    tools {
        maven 'Maven-Local'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/sivanandan21/maven-demo.git'
            }
        }

        stage('Maven Version') {
            steps {
                sh 'mvn -version'
            }
        }

        stage('Clean') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Unit Testing') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }
    }

    post {

        success {
            echo 'Maven build completed successfully!'
        }

        failure {
            echo 'Maven build failed. Check the console output.'
        }

        always {
            junit 'target/surefire-reports/*.xml'
        }
    }
}
