pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage('GitHub Clone') {
            steps {
                git url: 'https://github.com/Prashant4358/saidemytrend.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean deploy'
            }
        }
        stage('SonarQube analysis') { 
            environment {
                scannerHome = tool 'saidemy-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('saidemy-sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
