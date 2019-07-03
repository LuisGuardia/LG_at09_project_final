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
                sh './sampleWebApp/gradlew assemble -p sampleWebApp/'
                archiveArtifacts 'sampleWebApp/build/libs/*.jar'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Execute code analysis....'
                sh './sampleWebApp/gradlew check -p sampleWebApp/'
            }            
        }  
        stage('SonarQube') {
            steps {
                echo 'Execute 'sonar cube'
                sh './sampleWebApp/gradlew sonarcube -p sampleWebApp/'
            }            
        }
    } 
    post {
        always {
            mail to: 'g.luisalberto68@gmail.com',
            subject: "Successfull Pipeline: ${currentBuild.fullDisplayName}",
            body: "The pipeline ${env.BUILD_URL} completed successfully."
        }
    }
}

