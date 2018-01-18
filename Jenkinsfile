pipeline {
    agent none
    environment { 
      CC = 'clang'
    }
    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
    }
    stages {
        stage('Build') {
            agent any
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            agent {
                label 'linux'
            }
            steps {
                sh "echo 'Testing..' || false"
            }
        }
        stage('JenkinsEnvVars') {
            agent any
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            }
        }
        stage('EnvironmentVars') {
            agent any
            environment { 
                DEBUG_FLAGS = '-g'
            }
            steps {
                sh 'printenv'
            }
        }
        stage('Parameters') {
            agent any
            steps {
                echo "${params.Greeting} World!"
            }
        }
        stage('Deploy') {
            agent any
            steps {
                echo 'Deploying....'
            }
        }
        stage('Deploy2') {
            agent any
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                sh 'echo publish'
            }
        }
    }
    post {
        always {
            sh "echo always"
        }
        success {
                sh 'echo success'
        }
        unstable {
                sh 'echo unstable'
        }
        failure {
            sh 'echo failure'
        }
    }
}

