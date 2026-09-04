pipeline {
    agent any

    tools {
        ant 'Ant'
        jdk 'java21'
    }

    stages {

        stage('Clean') {
            steps {
                sh 'ant -f banking-devops-pipeline-master/demo1/build.xml clean'
            }
        }

        stage('Build') {
            steps {
                sh 'ant -f banking-devops-pipeline-master/demo1/build.xml build'
            }
        }

        stage('Test') {
            steps {
                sh 'ant -f banking-devops-pipeline-master/demo1/build.xml Debt_CalculationTest'
            }
        }

        stage('Junit reports') {
            steps {
                sh 'ant -f banking-devops-pipeline-master/demo1/build.xml junitreport'
            }
        }

        stage('Mutation Testing') {
            steps {
                sh 'ant -f banking-devops-pipeline-master/demo1/build.xml pit'
            }
        }

        stage('Find Bugs') {
            steps {
                sh 'ant -f banking-devops-pipeline-master/demo1/build.xml spotbugs'
            }
        }
    }
}
