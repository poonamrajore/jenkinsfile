pipeline {
    agent any
    
    stages {
        
        stage ('Git-Pull') {
            steps {
                git branch: 'devops', url: 'https://github.com/shubhamkalsait/EasyCRUD.git'
            }
        }
         stage ("Build") {
            steps {
                sh '''
                cd backend
                mvn clean package -DskipTests'''
            }
        }
         stage ("Test") {
            steps {
               withSonarQubeEnv(installationName: 'sonarqube' , credentialsId: 'sonar-cred') {
                        sh '''
                        cd backend
                        mvn sonar:sonar -Dsonar.projectKey=studentapp '''
                    }
            }
        }

        stage ("QualityGate") {
            steps {
                    timeout(10) {
                             waitForQualityGate abortPipeline: true, credentialsId: 'sonar-cred'
                        }
            }
        }
    }
