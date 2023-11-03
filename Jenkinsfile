pipeline {
    agent none
    tools {
        maven 'maven' 
    }
    parameters {
        string(name: 'rosh', defaultValue: 'test', description: 'env to compile') 
        booleanParam(name: 'executeTests', defaultValue: true, description: 'decide to run')
        choice(name: 'APPVERSION', choices: ['1.1', '1.2', '1.3'])
    }
    environment {
        DEV_SERVER= 'ec2-user@172.31.38.156'
    }
    stages {
        stage('compile') {
            agent any
            steps {
                script {
                    echo 'compile hello'
                    echo "compile in rosh: ${params.rosh}" 
                    sh "mvn compile"
                }
            }
        }
        stage('unit test') {
            agent any
            when {
                expression {
                    params.executeTests == true
                }
            }
            steps {
                script {
                    echo 'unittest hello'
                    sh "mvn test"
                }
            }
        }
        stage('package') {
            agent any
            steps {
                script {
                    sshagent (['roshan']) {
                        echo 'package hello'
                        echo "packaging the code version ${params.APPVERSION}"
                        sh "scp -o StrictHostKeyChecking=no server-config.sh ${DEV_SERVER}:/home/ec2-user"
                        sh "ssh -o StrictHostKeyChecking=no ${DEV_SERVER} 'bash ~/server-config.sh'"
                    }
                }
            }
        }
        stage('deploy') {
            agent any
            input {
                message "select the version to display"
                ok "version selected"
                parameters {
                    choice(name: 'newversion', choices: ['2.1', '2.2', '2.3'])
                }
            }
            steps {
                script {
                    echo 'deploy the app'
                }
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }
}
