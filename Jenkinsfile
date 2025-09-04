pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time:30, unit:'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    environment {
        def appVersion = ''
    }
    stages {
        stage('read version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "application version is : ${appVersion}"
                }
                
            }
        }
        stage('Install Dependencies') {
            steps {
                sh """
                 npm install
                 ls -ltr
                 echo "application version in stage id : ${appVersion}"
                 
                """
            }
        }
        stage('Build') {
            steps {
                sh """
                zip -q -r backend-${appVersion}.zip * -x Jenkinsfile -x backend-${appVersion}.zip
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