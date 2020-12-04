pipeline {
    agent {
        label 'Tomcat'
    }
    tools {
        maven 'Maven'
    }
    stages {
        stage ('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '**']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Aravindkrishnans/web_app.git']]])
            }
        }
        stage ('build') {
            steps {
                sh "mvn clean install"
            }
        }
        stage('deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'Tomcat', path: '', url: 'http://13.127.11.245:8080/')], contextPath: 'web_apps_01', war: '**/*.war'
            }
        }
    }
post {
    success {
        echo "The Build is success"
    }
}
}
