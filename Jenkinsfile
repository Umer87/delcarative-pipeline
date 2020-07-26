pipeline {
    agent any

    triggers {
       pollSCM("* * * * *")
       upstream(upstreamProjects:'project1', threshold: hudson.model.Result.SUCCESS)
    }

    stages {
        stage('Compile') {
            steps {
                sh 'echo Hello World'
                exit 1
            }
        }
        stage('Test') {
            steps {
                sh 'echo Test'
        
            }
        }
    }

    post {
        always {
             slackSend channel: '#devopsjune', message: env.BUILD_ID + 'Completed'
        }
        changed {
             sh 'echo build changed'
        }
        fixed {
            sh 'echo wohha build is not fixed'
        }
        failure {
            slackSend channel: '#devopsjune', message: $env.BUILD_ID + 'Failed'
        }
        success {
            sh 'echo Project is successfull'
        }
        unstable {
             slackSend channel: '#devopsjune', message: $env.BUILD_ID + 'Failed'
        }
    }
}