pipeline {
    agent any
    environment { 
      CC = 'clang'
    }
    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                sh "echo 'Testing..' || false"
            }
        }
        stage('JenkinsEnvVars') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            }
        }
        stage('EnvironmentVars') {
            environment { 
                DEBUG_FLAGS = '-g'
            }
            steps {
                sh 'printenv'
            }
        }
        stage('Parameters') {
            steps {
                echo "${params.Greeting} World!"
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
    post {
            always {
                sh "echo always"
            }
            failure {
                sh 'echo failure'
            }
        }
}

