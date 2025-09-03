pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time:30, unit:'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh """
                 npm install
                 ls -ltr
                """
            }
        }
    }
    post {
        always {
            echo "this will run always"
            deleteDir()
        }
        success {
            echo "this will run when pipeline is success"
        }
        failure {
            echo "this will run when pipeline is failed"
        }
    }
}