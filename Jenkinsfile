pipeline {
    agent{
        label 'linux'
    }

    tools {
        git 'GIT-2.42.0'
        terraform 'Terraform-1.5.0'
    }

    parameters {
        string(name: 'ENV', defaultValue: 'dev', description: 'Select environment')
        booleanParam(name: 'DEPLOY', defaultValue: true, description: 'Deploy the app?')
        choice(name: 'REGION', choices: ['us-east-1', 'us-west-2'], description: 'AWS Region')
        password(name: 'SECRET', defaultValue: '', description: 'Enter secret key')
        text(name: 'NOTES', defaultValue: '', description: 'Additional notes')
    }
    
    environment {
        Name = "CSI"
        env = "Dev"
        NEW_VER = '1.30'
    }
    
    stages {
        stage('git clone'){
            steps {
                retry(3) {
                    git branch: 'master', url: 'https://github.com/iam-SivaManikanta/jenkins.git'
                }
            }
            post {
                success {
                    echo 'Clone Successful'
                    echo "${env.env} is ready"
                    echo "Branch: ${env.GIT_BRANCH}, Build Number: ${env.BUILD_NUMBER}"
                }
                failure {
                    echo 'clone not done'
                }
            }
        }
        stage('changing directory') {
            steps {
                dir('abc') {
                    sh 'cat abc.py'
                }
            }
        }
        stage('Test') {
            steps {
                sh 'git --version'
                sh 'terraform --version'
                sh 'echo $PATH'
                sh 'which terraform'
                sh 'terraform --version'
            }
        }
        stage('Print Parameters') {
            steps {
                echo "Environment: ${params.ENV}"
                echo "Deploy: ${params.DEPLOY}"
                echo "Region: ${params.REGION}"
                echo "Secret: ${params.SECRET}"
                echo "Notes: ${params.NOTES}"
            }
        }
        stage('script checking') {
            steps {
            script {
                def buildStatus = "SUCCESS"
                    if (buildStatus == "SUCCESS") {
                        echo "Build was successful!"
                    } else {
                        echo "Build failed!"
                    }
            }
        }
    
    }
    }
    post {
        always {
            echo 'yeah always runs right'
            echo " The Version is ${env.NEW_VER} "
        }
        success {
            echo 'Yeah Success'
        }
        failure {
            echo 'Yeah Failed'
        }
    }
}
