pipeline 
{
  agent any
  stages
  {
    stage('Build')
    {
      steps
      {
         sh 'docker build -t nithyak12/nginx:nginx1.0 .'
      }
    }
    stage('Docker Push') {
    	agent any
      steps {
      	withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push nithyak12/nginx:nginx1.0'
        }
      }
    }
    stage('Docker deploy') {
    	agent any
      steps {
          withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker image rm -f nithyak12/nginx:nginx1.0'
          sh 'docker pull nithyak12/nginx:nginx1.0'
          sh 'docker run -d -p 9091:8080 nithyak12/nginx:nginx1.0'
          
        }
      }
    
    }
  }
}
