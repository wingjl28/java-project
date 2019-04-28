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
       withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AKIAJJWBDJMHNDMGY27Q', credentialsId: 'AWS user for Jenkins', secretKeyVariable: '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']]) {
            sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
        }	
    }
}

