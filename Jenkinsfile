pipeline {
    agent any 
    stages {
        stage ('git pull') {
            steps {
            git branch : 'main' , url: 'https://github.com/shubhamkalsait/EasyCRUD.git'
            echo "git pull successful"
        }
}
  stage ('build') {
      steps {
          sh '''
          cd backend 
          echo "build successful"
          '''
      }
  }
  stage ('test') {
      steps {
        withSonarQubeEnv(installationName: 'sonarqube', credentialsId: 'sonar-cred') {
    sh '''
    mvn sonar:sonar
     -Dsonar.projectKey=studentapp
    '''
          echo "test successful"
        }
      }
  }
  stage ('QualityGate') {
      steps {
      waitForQualityGate abortPipeline: false, credentialsId: 'sonar-cred'
  }
  }    
   stage ('deploy') {
       steps {
           echo "deploy successful"
       } 
}
}
}
