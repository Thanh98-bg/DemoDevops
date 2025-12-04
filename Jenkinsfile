pipeline {
    agent any
    environment {
        BRANCH_NAME = 'feature/depops'
    }

    stages {
        stage('Auto Merge') {
            steps {
                deleteDir() 
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'webhooktoken', url: 'https://github.com/Thanh98-bg/DemoDevops.git']])
                withCredentials([usernamePassword(credentialsId: 'webhooktoken', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh 'git config user.email "jenkins@example.com"'
                    sh 'git config user.name "Jenkins Auto Merge"'
                    sh 'git checkout master'
                    sh 'git pull origin master'
                    sh "git merge --no-ff origin/${env.BRANCH_NAME}"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/Thanh98-bg/DemoDevops.git master" 
                }
            }
        }
    }
}
