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
        sh 'docker build -t asignementrepo .'
         sh 'docker tag asignementrepo:latest 554283927585.dkr.ecr.us-east-1.amazonaws.com/asignementrepo:latest'
		 sh 'docker push 554283927585.dkr.ecr.us-east-1.amazonaws.com/asignementrepo:latest'
      }
    } 

     stage('Deploy') {
             steps {
                 sh 'ssh root@10.0.3.24 "docker pull 554283927585.dkr.ecr.us-east-1.amazonaws.com/asignementrepo:latest;"'
	             sh 'ssh root@10.0.3.24 "docker container rm -f nodeapp > /dev/null 2>&1;"'
	             sh 'ssh root@10.0.3.24 "docker container run -itd --name nodeapp -p 8080:8080 554283927585.dkr.ecr.us-east-1.amazonaws.com/asignementrepo;"'
             }
         }
  }
}
