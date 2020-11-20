#!groovy
 
import groovy.json.JsonSlurperClassic


node {
	def SF_CONSUMER_KEY=env.SF_CONSUMER_KEY
	def SF_USERNAME=env.SF_USERNAME
	def SERVER_KEY_CREDENTALS_ID=env.SERVER_KEY_CREDENTALS_ID
	def TEST_LEVEL='RunLocalTests'
	def PACKAGE_NAME='0Ho1U000000CaUzSAK'
	def PACKAGE_VERSION = 'version-1.0'
	def SF_INSTANCE_URL = env.SF_INSTANCE_URL ?: "https://login.salesforce.com"
	def SF_WORKSPACE = env.WORKSPACE
	
    // def toolbelt = tool 'toolbelt'
	// def toolbelt = tool 'toolbelt'
	stage('checkout source'){
		checkout scm
	}
	echo 'stage begins ==> '
    echo SF_WORKSPACE
	// -------------------------------------------------------------------------
    // Run all the enclosed stages with access to the Salesforce
    // JWT key credentials.
    // -------------------------------------------------------------------------
	// withEnv(["HOME=${env.WORKSPACE}"]) {
	// 	withCredentials([file(credentialsId: SERVER_KEY_CREDENTALS_ID, variable: 'server_key_file')]) {
		// -------------------------------------------------------------------------
        // Authorize the Dev Hub org with JWT key and give it an alias.
        // -------------------------------------------------------------------------
		stage('Authorize DevHub') {
				// def auth_command = "sfdx force:auth:jwt:grant \
				// --instanceurl ${SF_INSTANCE_URL} \
				// --clientid ${SF_CONSUMER_KEY} \
				// --username ${SF_USERNAME} \
				// --jwtkeyfile ${server_key_file} \
				// --setdefaultdevhubusername --setalias HubOrg"
    //             def auth_command = "sfdx --version"
				// // rc = command auth_command
    //             rc = command "sfdx --version"
    //             echo rc
                // if (rc != 0) {
                //     error 'Salesforce dev hub org authorization failed.'
                // }
                echo 'hello'
				
            }

			// -------------------------------------------------------------------------
            // Create new scratch org to test your code.
            // -------------------------------------------------------------------------
 
            // stage('Create Test Scratch Org') {
            //     sleep 10
            //     rc = command "sfdx force:org:create --targetdevhubusername HubOrg --setdefaultusername --definitionfile config/project-scratch-def.json --setalias ciorg --wait 10 --durationdays 1"
            // }

			// -------------------------------------------------------------------------
            // Display test scratch org info.
            // -------------------------------------------------------------------------
 
            // stage('Display Test Scratch Org') {
            //     sleep 10
            //     rc = command "sfdx force:org:display --targetusername ciorg"
            // }

			// -------------------------------------------------------------------------
            // Push source to test scratch org.
            // -------------------------------------------------------------------------
 
            // stage('Push To Test Scratch Org') {
            //     sleep 10
            //     rc = command "sfdx force:source:push --targetusername ciorg"
            // }

			// -------------------------------------------------------------------------
            // Run unit tests in test scratch org.
            // -------------------------------------------------------------------------
 
            // stage('Run Tests In Test Scratch Org') {
            //     sleep 10
            //     rc = command "sfdx force:apex:test:run --targetusername ciorg --wait 10 --resultformat tap --codecoverage --testlevel ${TEST_LEVEL}"
            // }

			// -------------------------------------------------------------------------
            // Delete test scratch org.
            // -------------------------------------------------------------------------
 
            // stage('Delete Test Scratch Org') {
            //     sleep 10
            //     rc = command "sfdx force:org:delete --targetusername ciorg --noprompt"
            // }

			// -------------------------------------------------------------------------
            // Create package version.
            // -------------------------------------------------------------------------
 
            // stage('Create Package Version') {
            //     sleep 10
            //     if (isUnix()) {
            //         // output = sh returnStdout: true, script: "sfdx force:package:version:create --package ${PACKAGE_NAME} --installationkeybypass --wait 10 --json --targetdevhubusername HubOrg"
            //     } else {
            //         // output = bat(returnStdout: true, script: "sfdx force:package:version:create --package ${PACKAGE_NAME} --installationkeybypass --wait 10 --json --targetdevhubusername HubOrg").trim()
            //         // output = output.readLines().drop(1).join(" ")
            //     }
 
            //     // Wait 5 minutes for package replication.
            //     sleep 30
 
            //     // def jsonSlurper = new JsonSlurperClassic()
            //     // def response = jsonSlurper.parseText(output)
 
            //     // PACKAGE_VERSION = response.result.SubscriberPackageVersionId
 
            //     response = null
 
            //     // echo ${PACKAGE_VERSION}
            // }

			// -------------------------------------------------------------------------
            // Create new scratch org to install package to.
            // -------------------------------------------------------------------------
 
    //         stage('Create Package Install Scratch Org') {
    //             rc = command "sfdx force:org:create --targetdevhubusername HubOrg --setdefaultusername --definitionfile config/project-scratch-def.json --setalias installorg --wait 10 --durationdays 1"
				// sleep 30
    //         }

			// -------------------------------------------------------------------------
            // Display install scratch org info.
            // -------------------------------------------------------------------------
 
            // stage('Display Install Scratch Org') {
            //     sleep 10
            //     rc = command "sfdx force:org:display --targetusername installorg"
            // }

			// -------------------------------------------------------------------------
            // Install package in scratch org.
            // -------------------------------------------------------------------------
 
            // stage('Install Package In Scratch Org') {
            //     rc = command "sfdx force:package:install --package ${PACKAGE_VERSION} --targetusername installorg --wait 10"
            // }

			// -------------------------------------------------------------------------
            // Run unit tests in package install scratch org.
            // -------------------------------------------------------------------------
 
            // stage('Run Tests In Package Install Scratch Org') {
            //     sleep 10
            //     rc = command "sfdx force:apex:test:run --targetusername installorg --resultformat tap --codecoverage --testlevel ${TEST_LEVEL} --wait 10"
            // }

			// -------------------------------------------------------------------------
            // Delete package install scratch org.
            // -------------------------------------------------------------------------
            // stage('Delete Package Install Scratch Org') {
            //     sleep 5
            //     rc = command "sfdx force:org:delete --targetusername installorg --noprompt"
            // }
		// }

	// }
	
}

def command(script) {
    if (isUnix()) {
        return sh(returnStatus: true, script: script);
    } else {
        return bat(returnStatus: true, script: script);
    }
}