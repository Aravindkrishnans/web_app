
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
                deploy adapters: [tomcat9(credentialsId: 'Tomcat', path: '', url: 'http://13.233.227.33:8080/')], contextPath: 'web_apps_01', war: '**/*.war'
            }
        }
    }
post {
    success {
        echo "The Build is success"
        node ('Tomcat') {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Aravindkrishnans/branch_test.git']]])
            sh "mvn clean install"
            deploy adapters: [tomcat9(credentialsId: 'Tomcat', path: '', url: 'http://13.233.227.33:8080/')], contextPath: 'test_01', war: '**/*.war'        
        }
    }
    aborted {
        echo "The Build is failed"
        node ('Tomcat') {
            checkout([$class: 'GitSCM', branches: [[name: '*/dev']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Aravindkrishnans/branch_test.git']]])
            sh "mvn clean install"
            deploy adapters: [tomcat9(credentialsId: 'Tomcat', path: '', url: 'http://13.233.227.33:8080/')], contextPath: 'abort_01', war: '**/*.war'
        }
    }
}
}
