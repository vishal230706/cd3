pipeline {
    agent any

    tools {
        jdk 'JDK17'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out Banking System source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling Java source files...'

                sh '''
                    rm -rf build
                    mkdir -p build

                    find src -name "*.java" > sources.txt

                    javac -d build @sources.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running basic Java validation...'

                sh '''
                    java -version
                    find build -name "*.class" | head
                '''
            }
        }

        stage('Package') {
            steps {
                echo 'Creating application JAR...'

                sh '''
                    jar cf BankingSystem.jar -C build .
                '''
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'BankingSystem.jar',
                                 fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Banking System build completed successfully!'
        }

        failure {
            echo 'Banking System build failed.'
        }

        always {
            echo 'Jenkins pipeline execution completed.'
        }
    }
}
