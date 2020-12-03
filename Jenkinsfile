pipeline {
    agent any

    stages {
        stage('CheckOut') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '**']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Aravindkrishnans/web_app.git']]])
            }
        }
        stage('mvn_build'){
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'db784e8f-45c7-42f3-908e-222cfec50bdd', path: '', url: 'http://13.233.34.227:8080')], contextPath: 'web_apps', war: '**/*.war'
            }
        }
    }
}
