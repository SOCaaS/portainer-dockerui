pipeline {
    agent any

    stages {
        stage('Install') {
            steps {
                echo 'Installing....'
                sh 'curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose'
                sh 'chmod +x /usr/bin/docker-compose'
                sh '/usr/bin/docker-compose --version'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh '/usr/bin/docker-compose -p "portainerdockerui" up -d --build'
            }
        }
    }
    post {
        success {
            discordSend description: "Build Success", footer: "Filebeat Service", link: env.BUILD_URL, result: currentBuild.currentResult, title: JOB_NAME, webhookURL: env.SOCAAS_WEBHOOK
        }
        failure {
            discordSend description: "Build Failed", footer: "Filebeat Service", link: env.BUILD_URL, result: currentBuild.currentResult, title: JOB_NAME, webhookURL: env.SOCAAS_WEBHOOK
        }
    }
}
