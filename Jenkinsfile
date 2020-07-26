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
            }
        }
    }

    post {
        always  {
            sh 'echo build completed'
        }
        changed {
             sh 'echo build changed'
        }
    }
}