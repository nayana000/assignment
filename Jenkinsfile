pipeline {
    agent any
    parameters {
        choice(name: 'environment', choices: ['dev', 'prod'])
        string(name: 'version', defaultValue: '1.0')
    }
    stages {
        stage('build') {
            steps {
                echo "Building"
            }
        }
        stage('test') {
            steps {
                echo "testing"
            }
        }
        stage('deploy') {
            steps {
                echo "Deploying"
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: '*.txt', fingerprint: true
            script {
                currentBuild.description = "environment: ${params.environment}, version: ${params.version}"
            }
            build job: 'deploy-job', wait: false
        }
    }
}
