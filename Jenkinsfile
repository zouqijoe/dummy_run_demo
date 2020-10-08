#!/usr/bin/env groovy
// import java.util.regex.Pattern
pipeline {
    agent any

    options{
        timeout(time: 5, unit: 'MINUTES') //timeout all agents on pipeline if not complete
    }

    parameters {
        gitParameter(branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'source_branch', type: 'PT_BRANCH', description: 'Select a branch to build from')
        choice(name: 'target_environment',
            choices: getSFEvnParams(),
            description: 'Select a Salesforce Org to build against')
        booleanParam(name: 'validate_only_deploy',
            defaultValue: true,
            description: 'Check this to run a validate only deploy')
        choice(name: 'test_level',
            choices: 'NoTestRun\nRunSpecifiedTests\nRunLocalTests',
            description: 'Set the Test Level for this Build')
        string(name: 'specified_tests',
            defaultValue: 'ex: ClassTest,Class2Test',
            description: 'If Test Level is "RunSpecifiedTests" then specify a comma seperated list of test classes to run. Ex: "AccountTriggerHandlerTest,LeadTriggerHandlerTest"')
    }

    stages{
        stage('Initialize Pipeline'){
            steps{
                echo "Initializing"
                // determine if the build was trigger from a git event or manually built with parameters
                echo "${currentBuild.buildCauses}"
                // all current build environment variables
                echo sh(returnStdout: true, script: 'env')
                echo "env setupRunning ${env.BUILD_ID} on ${env.JENKINS_URL}"
		        echo "something to print out"
                envSetup()
            }
        }
        stage('Github Sync'){
            steps{
                echo "hello!"
                echo "Github Sync"
                githubCheckout()
            }
        }
        stage('SFDX Auth Target Org') {
            steps {
                authSF()
            }
        }
        stage('SFDX Deploy'){
            steps{
                echo "Deploy Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                //TODO:
                // salesforceDeploy()
                //sfdx commands
            }
        }
    }
}

def githubCheckout(){
    dir('github-checkout'){
        checkout scm

        commitChangeSet = sh(returnStdout: true, script: 'git diff-tree --no-commit-id --name-only -r HEAD')
        echo "github-checkout"
        echo "${commitChangeSet}"
        echo "${commitChangeSet.size()}"
    }

    echo "#######################################"
    echo "#######################################"
    echo "#######################################"
    echo "#######################################"
    echo "#######################################"

    sh 'ls github-checkout'
    echo "Current Git Commit : ${env.GIT_COMMIT}"
    echo "Previous Known successful Git commit: ${env.GIT_PREVIOUS_SUCCESSFUL_COMMIT}"
}

// def githubCheckout() {
//     dir('github-checkout') {
//         // determine if the build was trigger from a git event or manually built with parameters
//         if ("${currentBuild.buildCauses}".contains("UserIdCause")) {
//             echo "git checkout ${params.source_branch}"
//             // git checkout the branch
//             git credentialsId: 'pwId', url:'repoUrl', branch: "${params.source_branch}"
//         }
//         else if("${currentBuild.buildCauses}".contains("BranchEventCause")) {
//             echo "git checkout ${env.BRANCH_NAME}"
//             checkout scm
//         }
//     }

//     sh 'ls github-checkout'
//     echo "Current GIT Commit : ${env.GIT_COMMIT}"
//     echo "Previous Known Successful GIT Commit : ${env.GIT_PREVIOUS_SUCCESSFUL_COMMIT}"
// }

def getSFEvnParams() {
    echo "getSFEnvParams"
    def fields = env.getEnvironment()
    def output = "";
    fields.each {
        key, value -> if("${key}".startsWith("SFDX_")) { output += "${key}\n"; }
    }
    return output;
}

def envSetup(){
    echo "initDeployEnvRunning ${env.BUILD_ID} on ${env.JENKINS_URL}"
    echo sh(returnStdout: true, script: 'env')
    echo "${BUILD_URL}"
    echo "#######################################"
    echo "#######################################"
    def CHANGE_TARGET = env.CHANGE_TARGET
    echo "#######################################"
    // echo "#######################################"
}

def authSF() {
    echo 'SF Auth method'
    def SF_AUTH_URL
    echo env.BRANCH_NAME
    echo 'XXXXXXXXXXXXX'
    echo env
    // if ("${currentBuild.buildCauses}".contains("UserIdCause")) {
    //     def fields = env.getEnvironment()
    //     fields.each {
    //         key, value -> if("${key}".contains("${params.target_environment}")) { SF_AUTH_URL = "${value}"; }
    //     }
    // }
    // else if("${currentBuild.buildCauses}".contains("BranchEventCause")) {
    //     if(env.BRANCH_NAME == 'master' || env.CHANGE_TARGET == 'master') {
    //         SF_AUTH_URL = env.SFDX_DEV
    //     }
    //     else { // {PR} todo - better determine if its a PR env.CHANGE_TARGET?
    //         SF_AUTH_URL = env.SFDX_DEV
    //     }
    // }
    // echo 'SF_AUTH_URL: '
    // echo SF_AUTH_URL
    // writeFile file: 'authjenkinsci.txt', text: SF_AUTH_URL
    // sh 'ls -l authjenkinsci.txt'
    // sh 'cat authjenkinsci.txt'
    // echo 'end sf auth method'
}

def command(script) {
   if (isUnix()) {
       return sh(returnStatus: true, script: script);
   } else {
       return bat(returnStatus: true, script: script);
   }
}
