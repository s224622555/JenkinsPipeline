pipeline{
    agent any
    environment{
        BUILD_AUTOMATION_TOOL="Gradle"
        TEST_AUTOMATION_TOOL="Katalon"
        CODE_ANALYSIS_TOOL="GitHub"
        SECURITY_SCAN_TOOL="ZAP"
        STAGING_SERVER="STAGING_SVR"
        PRODUCTION_SERVER="PROD_SVR"
    }
    stages{
        stage('Build'){
            steps{
                echo "Build the source code using $BUILD_AUTOMATION_TOOL to compile and package code"
            }
        }
        stage('Unit and Integration Tests'){
            steps{
                echo "Run unit tests using $TEST_AUTOMATION_TOOL"
                echo "Run integration tests using $TEST_AUTOMATION_TOOL"
            }
             post{
                success{
                    emailext(attachLog: true, body: 'Success: source code and components of the application work together as expected', 
                             subject: 'Unit and Integration Tests Success', to: 'tammie.shepperd@gmail.com')
                } 
                failure{
                    emailext(attachLog: true, body: 'Failure: issue with source code or the application',
                        subject: 'Unit and Integration Tests Failure', to: 'tammie.shepperd@gmail.com')
                }
            } 
        }
        stage('Code Analysis'){
            steps{
                echo " Analyse the source code using $CODE_ANALYSIS_TOOL to ensure it meets industry standards"
            }
        }
        stage('Security Scan'){
            steps{
                echo "Perform security scan using $SECURITY_SCAN_TOOL"
            }
             post{
                success{
                    emailext(attachLog: true, body: 'Success: source code meets industry standards', 
                             subject: 'Security Scan Success', to: 'tammie.shepperd@gmail.com')
                }
                failure{
                    emailext(attachLog: true, body: 'Failure: source code does not meet industry standards', 
                             subject: 'Security Scan Failure', to: 'tammie.shepperd@gmail.com')
                }
            }
        }
        stage('Deploy to Staging'){
            steps{
                echo "Deploy the application to $STAGING_SERVER"
            }
        }
        stage('Integration Tests on Staging'){
            steps{
                echo "Run integration tests on the staging environment"
            }
             post{
                success{
                    emailext(attachLog: true, body: 'Success: application functions as expected in a production-like environment', 
                             subject: 'Integration Tests on Staging Success', to: 'tammie.shepperd@gmail.com')
                }
                failure{
                    emailext(attachLog: true, body: 'Failure: application does not function as expected in a production-like environment', 
                             subject: 'Integration Tests on Staging Failure', to: 'tammie.shepperd@gmail.com')
                }
            }
        }
        stage('Deploy to Production'){
            steps{
                echo "Deploy the application to $PRODUCTION_SERVER"
            }
        }
    }
}