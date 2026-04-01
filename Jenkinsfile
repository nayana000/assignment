pipeline {
    agent { label 'node2' }
    parameters {
        choice(name: 'environment', choices: ['dev', 'prod'])
        string(name: 'version', defaultValue: '1.0')
    }
    triggers{
        parameterizedCron('''
        */5 * * * * %environment=dev
        */5 * * * * %environment=prod
        ''')
    }
    stages {
        stage('build') {
            steps {
                echo "Building version ${params.Version} for ${params.Environment}"
                sh 'echo "Build complete" > build.txt'
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
