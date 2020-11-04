#!groovy
 
import groovy.json.JsonSlurperClassic


node {
	def SF_CONSUMER_KEY=env.SF_CONSUMER_KEY
	def SF_USERNAME=env.SF_USERNAME
	def SERVER_KEY_CREDENTALS_ID=env.SERVER_KEY_CREDENTALS_ID
	def TEST_LEVEL='RunLocalTests'
	def PACKAGE_NAME='0Ho1U000000CaUzSAK'
	def PACKAGE_VERSION
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
				def auth_command = "sfdx force:auth:jwt:grant \
				--instanceurl ${SF_INSTANCE_URL} \
				--clientid ${SF_CONSUMER_KEY} \
				--username ${SF_USERNAME} \
				--jwtkeyfile ${server_key_file} \
				--setdefaultdevhubusername --setalias HubOrg"
				rc = command auth_command
				// rc = command "sfdx force:auth:jwt:grant --instanceurl ${SF_INSTANCE_URL} --clientid ${SF_CONSUMER_KEY} --username ${SF_USERNAME} --jwtkeyfile ${server_key_file} --setdefaultdevhubusername --setalias HubOrg"
                // if (rc != 0) {
                //     error 'Salesforce dev hub org authorization failed.'
                // } else {
				// 	echo "OK"
				// }
				
            }

			// -------------------------------------------------------------------------
            // Create new scratch org to test your code.
            // -------------------------------------------------------------------------
 
            stage('Create Test Scratch Org') {
                rc = command "sfdx force:org:create --targetdevhubusername HubOrg --setdefaultusername --definitionfile config/project-scratch-def.json --setalias ciorg --wait 10 --durationdays 1"
                // if (rc != 0) {
                //     error 'Salesforce test scratch org creation failed.'
                // } else {
				// 	echo 'OK'
				// }
            }

			// -------------------------------------------------------------------------
            // Display test scratch org info.
            // -------------------------------------------------------------------------
 
            stage('Display Test Scratch Org') {
                rc = command "sfdx force:org:display --targetusername ciorg"
                // if (rc != 0) {
                //     error 'Salesforce test scratch org display failed.'
                // }
            }

			// -------------------------------------------------------------------------
            // Push source to test scratch org.
            // -------------------------------------------------------------------------
 
            stage('Push To Test Scratch Org') {
                rc = command "sfdx force:source:push --targetusername ciorg"
                // if (rc != 0) {
                //     error 'Salesforce push to test scratch org failed.'
                // }
            }

			// -------------------------------------------------------------------------
            // Run unit tests in test scratch org.
            // -------------------------------------------------------------------------
 
            stage('Run Tests In Test Scratch Org') {
                rc = command "sfdx force:apex:test:run --targetusername ciorg --wait 10 --resultformat tap --codecoverage --testlevel ${TEST_LEVEL}"
                // if (rc != 0) {
                //     error 'Salesforce unit test run in test scratch org failed.'
                // }
            }

			// -------------------------------------------------------------------------
            // Delete test scratch org.
            // -------------------------------------------------------------------------
 
            stage('Delete Test Scratch Org') {
                rc = command "sfdx force:org:delete --targetusername ciorg --noprompt"
                // if (rc != 0) {
                //     error 'Salesforce test scratch org deletion failed.'
                // }
            }

			// -------------------------------------------------------------------------
            // Create package version.
            // -------------------------------------------------------------------------
 
            stage('Create Package Version') {
                if (isUnix()) {
                    // output = sh returnStdout: true, script: "sfdx force:package:version:create --package ${PACKAGE_NAME} --installationkeybypass --wait 10 --json --targetdevhubusername HubOrg"
                } else {
                    output = bat(returnStdout: true, script: "sfdx force:package:version:create --package ${PACKAGE_NAME} --installationkeybypass --wait 10 --json --targetdevhubusername HubOrg").trim()
                    output = output.readLines().drop(1).join(" ")
                }
 
                // Wait 5 minutes for package replication.
                sleep 300
 
                def jsonSlurper = new JsonSlurperClassic()
                // def response = jsonSlurper.parseText(output)
 
                // PACKAGE_VERSION = response.result.SubscriberPackageVersionId
 
                response = null
 
                echo ${PACKAGE_VERSION}
            }
		}

	}
	
}
