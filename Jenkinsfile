pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                echo 'Building.'
            }
        }
        stage('Assemble') { 
            steps {
                echo 'Compiling.'
                sh 'chmod +x ./sampleWebApp/gradlew'
                sh './sampleWebApp/gradlew assemble -p sampleWebApp/'
                archiveArtifacts 'sampleWebApp/build/libs/*.jar'
            }
        }
        stage('Unit Test') {
            steps {
                echo 'Execute code analysis....'
                sh './sampleWebApp/gradlew test -p sampleWebApp/'
            } 
            post {
                always{
                    junit "sampleWebApp/build/test-results/test/*.xml"
                    archiveArtifacts 'sampleWebApp/build/reports/tests/test/*'
                }
            }           
        }
        stage('SonarQube') {
            steps {
                echo 'Execute sonar cube'
                sh './sampleWebApp/gradlew sonarqube -p sampleWebApp/'
            }            
        }
    } 
}

