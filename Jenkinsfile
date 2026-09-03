pipeline {
    agent any

    stages {

        stage('Run JMeter Test') {
            steps {
                bat '''
                    jmeter -n ^
                    -t swagger.jmx ^
                    -l swagger-result.jtl ^
                    -JUSERS=5
                '''
            }
        }

        stage('Generate HTML Report') {
            steps {
                bat '''
                    if exist html-report rmdir /S /Q html-report
                    jmeter -g swagger-result.jtl -o html-report
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'swagger-result.jtl', allowEmptyArchive: true
            archiveArtifacts artifacts: 'html-report/**', allowEmptyArchive: true
        }
    }
}