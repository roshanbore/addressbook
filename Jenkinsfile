pipeline {
    agent any
    parameters {
        string(name: 'rosh', defaultValue: 'test', description: 'env to compile') 
        booleanParam(name: 'executeTests', defaultValue: true, description: 'decide to run')
        choice(name: 'APPVERSION', choices: ['1.1', '1.2', '1.3'])
    }

    stages {
        stage('compile') {
            steps {
                script {
                    echo 'compile hello'
                    echo "compile in rosh: ${params.rosh}" 
                }
            }
        }
        stage('unit test') {
            when {
                expression {
                    params.executeTests == true
                }
            }
            steps {
                script {
                    echo 'unittest hello'
                }
            }
        }
        stage('package') {
            steps {
                script {
                    echo 'package hello'
                    echo "packaging the code version ${params.APPVERSION}"
                }
            }
        }
    }
}
