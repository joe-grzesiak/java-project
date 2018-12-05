properties([pipelineTriggers([githubPush()])])

node('linux') {   

	stage('Report') {    
		sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins' 
	}
}
