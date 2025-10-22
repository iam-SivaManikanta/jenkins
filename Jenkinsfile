pipeline {
    agent{
        label 'linux'
    }
    
    environment {
        Name = "CSI"
        env = "De"
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
                sh 'python3 --version'
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
