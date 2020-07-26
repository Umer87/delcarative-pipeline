pipeline {
    agent any

     tools {
        maven 'm3.6'
        java  'jdk8' 
    }

    triggers {
       pollSCM("* * * * *")
       upstream(upstreamProjects:'project1', threshold: hudson.model.Result.SUCCESS)
    }
    // parameters { 

    //         string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: '')
    //         choice(name: 'TARGET_ENV', choices: ['STAGING','PROD','QA'],  description: '') 
    
    // }

    options { 
            buildDiscarder(logRotator(numToKeepStr: '2')) 
            disableConcurrentBuilds()
            retry(2)
        
        }
    environment {
            JAVA_VERSION='1.8'
            GIT_HUB_CREDS = credentials('github');
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Compile') {
            environment {
                    JAVA_VERSION='1.7'
                    GIT_HUB_CREDS = credentials('github');
                }
            steps {
                sh 'mvn compile'
        
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
        
            }
        }
         stage('Package') {
            steps {
                sh 'mvn package'
        
            }
        }
    }

    post {
        always {
             slackSend channel: '#devopsjune', message:  env.BUILD_DISPLAY_NAME  + ' Completed'
        }
        changed {
             sh 'echo build changed'
    
        }
        fixed {
            sh 'echo wohha build is not fixed'
        }
        failure {
            slackSend channel: '#devopsjune', message: env.BUILD_ID + 'Failed'
        }
        success {
            sh 'echo Project is successfull'
        }
        unstable {
             slackSend channel: '#devopsjune', message: env.BUILD_ID + 'Failed'
        }
    }
}