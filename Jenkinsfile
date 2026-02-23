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
          echo "test successful"
      }
  }
   stage ('deploy') {
       steps {
           echo "deploy successful"
       } 
}
}
}
