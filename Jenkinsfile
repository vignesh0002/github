pipeline 
{
  agent any
  stages
  {
    stage('Build')
    {
      steps
      {
         sh 'docker build -t vignesh_nginx:1.1 .'
      }
    }

    stage('Docker deploy') {
    	agent any
      steps {
          sh 'docker run -d -p 9091:8080 vignesh_nginx:1.1'
          
        }
      }
    
  }
}
