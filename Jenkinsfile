properties([pipelineTriggers([githubPush()])])

node('linux') {
	stage('Unit Tests') {
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'
	}
	stage('Build') {
		sh 'ant -f build.xml -v'
	}
	stage('Deploy') {
		sh 'env|sort > rectangle-${BUILD_NUMBER}'
		sh 'aws s3 cp rectangle-${BUILD_NUMBER} s3://seis665-will-data/ '
	}
	stage('Report') {
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'dd396fb9-bc3a-49b5-a9b0-ae6b943d6731', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
			sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1'
		}
	}
}
