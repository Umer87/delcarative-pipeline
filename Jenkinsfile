pipeline {
    agent : any

    trigger {
        cron("* * * * *")
    }

    stages {
        stage('Compile') {
            steps {
                sh 'echo Hello World'
            }
        }
    }

    post: {
        always  {
            sh 'echo build completed'
        }
        changed {
             sh 'echo build changed'
        }
    }
}