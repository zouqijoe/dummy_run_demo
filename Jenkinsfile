#!/usr/bin/env groovy
// import java.util.regex.Pattern
pipeline {
    agent any

    options{
        timeout(time: 5, unit: 'MINUTES') //timeout all agents on pipeline if not complete
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

def envSetup(){
    echo "initDeployEnvRunning ${env.BUILD_ID} on ${env.JENKINS_URL}"
    echo sh(returnStdout: true, script: 'env')
    echo "${BUILD_URL}"
    echo "#######################################"
    echo "#######################################"
    def CHANGE_TARGET = env.CHANGE_TARGET
    echo "#######################################"
    echo "#######################################"
}
