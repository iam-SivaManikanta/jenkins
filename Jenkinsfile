pipeline {
    agent{
        label 'linux'
    }

    tools {
        git 'GIT-2.42.0'
        terraform 'Terraform-1.5.0'
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
        stage('Test') {
            steps {
                sh 'git --version'
                sh 'terraform --version'
                sh 'echo $PATH'
                sh 'which terraform'
                sh 'terraform --version'
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
