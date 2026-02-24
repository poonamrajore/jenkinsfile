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
               withSonarQubeEnv(installationName: 'Mysonar') {
                        sh '''
                        cd backend
                        mvn sonar:sonar -Dsonar.projectKey=studentapp '''
                    }
            }
        }

        stage ("QualityGate") {
            steps {
                     
                             waitForQualityGate abortPipeline: true
            }
        }
    
     stage ("S3-UPLOAD") {
       steps {
            sh 'aws s3 cp backend/target/*.jar s3://jenkins-s3-poonam/studentapp.jar'
     }
     }
}
}
