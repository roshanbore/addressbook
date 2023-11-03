pipeline {
    agent none
    tools {
        jdk 'jdk' // Use the actual tool name for Java
        maven 'maven' // Use the actual tool name for Maven
    }
    parameters {
        string(name: 'rosh', defaultValue: 'test', description: 'env to compile') 
        booleanParam(name: 'executeTests', defaultValue: true, description: 'decide to run')
        choice(name: 'APPVERSION', choices: ['1.1', '1.2', '1.3'])
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
        post {
            always {
                junit 'target/surefire-reports/*.xml'

        
        stage('package') {
            agent any
            steps {
                script {
                    sshagent (['aws-key']) {
                    echo 'package hello'
                    echo "packaging the code version ${params.APPVERSION}"
                    sh "mvn package"
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
        }
    }
}
