node {

	def to = emailextrecipients([
		[$class: 'CulpritsRecipientProvider'],
		[$class: 'DevelopersRecipientProvider'],
		[$class: 'RequesterRecipientProvider']
	])

	try {
		stage('build') {
			println('so far so good')
		}
		stage('test') {
			println('Aw crap')
			sh 'exit 1'
		}
	
	} catch(e) {
		currentBuild.result = "FAILURE";
		def subject = "${env.JOB_NAME} - Build #${env.BUILD_NUMBER} ${currentBuild.result}"
		def content = '${JELLY_SCRIPT,template="html"}'
	
		if( to != null && !to.isEmpty()) {
			emailext(body: content, mimeType: 'text/html',
				replyTo: '$DEFAULT_REPLYTO', subject: subject,
				to: to, attachLog: true )
		}
	
		throw e;
	}
}