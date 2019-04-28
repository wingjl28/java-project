properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    stage('Build'){
        git 'https://github.com/wingjl28/java-project.git'
        sh "ant"
        sh "ant -f build.xml -v"
    }
    
    stage('Test'){
        sh "ant -buildfile test.xml"
    }
    
    stage('Deploy'){
        
    }
    
    stage('Report'){
       withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AKIAUPKBPICG4KDQAA24', credentialsId: 'AWS user for jenkins', secretKeyVariable: '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']]) {
        sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
       }
    }
}

