#!groovy
 
import groovy.json.JsonSlurperClassic


node {
	echo 'hello'
	def SF_USERNAME=env.SF_USERNAME
	def SF_INSTANCE_URL = env.SF_INSTANCE_URL ?: "https://login.salesforce.com"
	def SF_WORKSPACE = env.WORKSPACE
	echo SF_USERNAME
	echo SF_INSTANCE_URL
	echo 'hello end'
	echo 'work space: '
	echo SF_WORKSPACE
	// def toolbelt = tool 'toolbelt'
	stage('checkout source'){
		checkout scm
	}
	echo 'stage begins ==> '
	// -------------------------------------------------------------------------
    // Run all the enclosed stages with access to the Salesforce
    // JWT key credentials.
    // -------------------------------------------------------------------------
	withEnv(["HOME=${env.WORKSPACE}"]) {
		echo 'withEnv hahaha'


	}
	
}
