pipeline {
    agent any

    stages {

        stage('Git Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                checkout scm
            }
        }

        stage('Check Java') {
            steps {
                sh '''
                    echo "Java version:"
                    java -version

                    echo "Javac version:"
                    javac -version
                '''
            }
        }

        stage('Build') {
            steps {
                dir('BankingSystem-master') {
                    sh '''
                        echo "Compiling Java source files..."

                        rm -rf build
                        mkdir -p build

                        find src -name "*.java" > sources.txt

                        javac -d build @sources.txt
                    '''
                }
            }
        }

        stage('Test') {
            steps {
                dir('BankingSystem-master') {
                    sh '''
                        echo "Checking compiled Java classes..."

                        find build -name "*.class"

                        if [ -z "$(find build -name '*.class')" ]; then
                            echo "No class files found!"
                            exit 1
                        fi

                        echo "Compilation successful!"
                    '''
                }
            }
        }

        stage('Package') {
            steps {
                dir('BankingSystem-master') {
                    sh '''
                        echo "Creating JAR file..."

                        jar cf BankingSystem.jar -C build .

                        ls -lh BankingSystem.jar
                    '''
                }
            }
        }

        stage('Archive') {
            steps {
                dir('BankingSystem-master') {
                    archiveArtifacts artifacts: 'BankingSystem.jar',
                                     fingerprint: true
                }
            }
        }
    }

    post {
        success {
            echo '======================================'
            echo ' Banking System build SUCCESSFUL!'
            echo '======================================'
        }

        failure {
            echo '======================================'
            echo ' Banking System build FAILED!'
            echo ' Check the Console Output.'
            echo '======================================'
        }

        always {
            echo 'Jenkins pipeline execution completed.'
        }
    }
}
