pipeline {
    agent any 
    
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    
    stages {
        stage('Build stage') {
            steps {
                echo ".....Build started"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "...build completed..."
            }
        }
        
        stage('Test') { 
            steps {
                echo "...testing started..."
                sh 'mvn surefire-report:report'
                echo ".....unit test completed"
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
