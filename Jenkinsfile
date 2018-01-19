pipeline {
    agent {
        label "master"
    }
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
        stage('Deploy2') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                sh 'echo publish'
            }
            post {
                always {
                    sh "echo always deploy"
                }
                success {
                        sh 'echo success deploy'
                }
                unstable {
                        sh 'echo unstable deploy'
                }
                failure {
                    sh 'echo failure deploy'
                }
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


