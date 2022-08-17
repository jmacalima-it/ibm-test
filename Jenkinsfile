pipeline {

  agent any
  
  environment {
  def dockerRun = 'docker run -d -p 80:8080 --name jenkins-php jmacalimait/nginx-test:php'
   
  }
    
    
  stages {
    
stage ('SCM checkout') {
  steps {
git branch: 'main', url: 'https://github.com/jmacalima-it/ibm-test.git'
  checkout scm
  }  
}
 
  
  stage ('Docker Image Build') {
    steps {
sh 'docker build -t nginx-phpinfo .'
sh 'docker tag nginx-phpinfo jmacalimait/nginx-test:php'
    }
}


  stage ('Push Docker image to DockerHub') {
    steps {
sh 'docker push jmacalimait/nginx-test:php'
    }
}
  
  
  stage ('Deploy to Dev') {   
    steps {
sshagent(['dserver']) {
  sh "ssh -o StrictHostKeyChecking=no ubuntu@52.53.43.187 ${dockerRun}"
}
 }
  }
      
    
}
 //end stages
}  
 //end of pipelines
