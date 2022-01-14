pipeline {
  agent any
    
  stages {
        
    stage('Git') {
      steps {
       git branch: 'main', url: 'https://github.com/rkgcsit/appcode.git'
      }
    }
     
    stage('Build') {
      steps {
        sh 'cd /var/lib/jenkins/workspace/nodeapp'
        sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 554283927585.dkr.ecr.us-east-1.amazonaws.com'  
        sh 'docker build -t aasignementrepo .'
         sh 'docker tag aasignementrepo:latest 554283927585.dkr.ecr.us-east-1.amazonaws.com/aasignementrepo:latest'
		 sh 'docker push 554283927585.dkr.ecr.us-east-1.amazonaws.com/aasignementrepo:latest'
      }
    }  
  }
}
