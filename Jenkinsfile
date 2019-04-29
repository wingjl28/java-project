properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    stage('Build'){
        git 'https://github.com/wingjl28/java-project.git'
        sh "ant -f build.xml -v"
  
    }
    
    stage('Unit Tests'){
        junit 'reports/result.xml'
        sh "ant -f test.xml -v"
    }
    

    
    stage('Report'){
       
       withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS user for Jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
       }
    }
    
    stage('Deploy'){

        sh "aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://seis665-jacobwing"
        
    }
}

