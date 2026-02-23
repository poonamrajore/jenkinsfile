pipeline {
    agent any 

    stages {

        stage('git pull') {
            steps {
                git branch: 'main', url: 'https://github.com/shubhamkalsait/EasyCRUD.git'
                echo "git pull successful"
            }
        }

        stage('build') {
            steps {
                sh '''
                cd backend
                mvn clean package
                '''
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                    cd backend
                    mvn sonar:sonar -Dsonar.projectKey=studentapp
                    '''
                }
            }
        }

        stage('QualityGate') {
            steps {
                waitForQualityGate abortPipeline: true 
            }
        }

        stage('deploy') {
            steps {
                echo "deploy successful"
            }
        }
    }
}
