pipeline {
    agent any
    
     tools {
        maven 'Maven'
    }

    stages {
        stage('pulling-source-code') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Ravi5515/Jenkinspractice.git']])
            }
        }
        stage('Run-tests'){
            parallel{
                stage('Sonar-scan'){
                    steps{
                        echo "sonar scan done"
                    }   
                }
                stage('unit-test'){
                    steps{
                        echo 'running unit test'
                    }   
                }
            }
        }

        stage('build-source-code') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('deploy-to-container') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat9', path: '', url: 'http://13.214.208.144:8080')], contextPath: '/app', war: '**/*war'
            }
        }
    }
}
