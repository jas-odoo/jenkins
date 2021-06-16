pipeline {
    agent any 
    stages {
        stage('Clone SCM') { 
            steps {
            	git '${GitRepoURL}'
                echo "Cloning Successful"
            }
        }
        stage('Build') { 
            steps {
                sh '''cd /var/jenkins_home/workspace/test_pipeline
                    python3 setup.py bdist_wheel'''
                echo "Test Successful"
            }
        }
        stage('Static Code Analysis') { 
            steps {
                //def scannerHome = tool 'SonarScanner 4.0';
                withSonarQubeEnv('sonarqube') {
                    sh "/var/jenkins_home/sonar-scanner-4.6.2.2472-linux/bin/sonar-scanner -Dsonar.projectKey=${ProjectNameSonarqube} -Dsonar.sources=/var/jenkins_home/workspace/test_pipeline/hello"
                }
                echo "Static Code Analysis Successful"
            }
        }
    }
}
