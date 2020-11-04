#!groovy
 
import groovy.json.JsonSlurperClassic


node {
	def SF_CONSUMER_KEY=env.SF_CONSUMER_KEY
	def SF_USERNAME=env.SF_USERNAME
	def SERVER_KEY_CREDENTALS_ID=env.SERVER_KEY_CREDENTALS_ID
	def TEST_LEVEL='RunLocalTests'
	def SF_INSTANCE_URL = env.SF_INSTANCE_URL ?: "https://login.salesforce.com"
	def SF_WORKSPACE = env.WORKSPACE
	
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
		withCredentials([file(credentialsId: SERVER_KEY_CREDENTALS_ID, variable: 'server_key_file')]) {
		// -------------------------------------------------------------------------
        // Authorize the Dev Hub org with JWT key and give it an alias.
        // -------------------------------------------------------------------------
		stage('Authorize DevHub') {
				echo SF_INSTANCE_URL
				echo SF_CONSUMER_KEY
				echo SF_USERNAME
				echo server_key_file
				// def auth_command = "sfdx force:auth:jwt:grant --instanceurl ${SF_INSTANCE_URL} --clientid ${SF_CONSUMER_KEY} --username ${SF_USERNAME} --jwtkeyfile ${server_key_file} --setdefaultdevhubusername --setalias DummyHubOrg"
				auth_command = "sfdx force:auth:jwt:grant --instanceurl https://login.salesforce.com \
				--clientid 3MVG9l2zHsylwlpT1BabsPgulAjRSggtH7kjhi3A7.8rpM4WH5U8Y1EgO0y_r_najCDLa.P4X3ygGrh9bPNOh \
				--username perfectionobsess@resilient-koala-2kki0f.com --jwtkeyfile ${server_key_file} \
				--setdefaultdevhubusername --setalias DummyHubOrg"
				
				rc = command auth_command
				// rc = command "sfdx force:auth:jwt:grant --instanceurl ${SF_INSTANCE_URL} --clientid ${SF_CONSUMER_KEY} --username ${SF_USERNAME} --jwtkeyfile ${server_key_file} --setdefaultdevhubusername --setalias DummyHubOrg"
                if (rc != 0) {
                    error 'Salesforce dev hub org authorization failed.'
                } else {
					echo "OK"
				}
				
            }
		}

	}
	
}
