properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Unit Tests') {    
		git 'https://github.com/joe-grzesiak/java-project.git'
		sh 'ant -f test.xml -v'   
		junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
	stage('Deploy') {
		archiveArtifacts artifacts: 'dist/*.jar', onlyIfSuccessful: true    
		sh 'aws s3 cp /dist/*.jar s3://seis665-03-fall2018-jgrz/'
	}
	stage('Report') {    
		sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins' 
	}
}
