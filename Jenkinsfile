pipeline {
    agent any
    parameters {
         string(name: 'rosh', defaultValue: 'test', description: 'env to compile') 
        booleanParam(name: 'executeTests', defaultValue: True, description: 'decide to run')
        choice(name: 'APPVERSION', choices: ['1.1', '1.2', '1.3'])
    
    }

    stages {
        stage('compile') {
            steps {
                script{
                echo 'compile hello'
                echo "compile in rosh: ${params.rosh}" 
            }
        }
        stage('unit test') {
            When{
                expression{
                    params.execute.Tests == True
            steps {
                script{
                echo 'unittest hello'
            }
        }
        stage('package') {
            steps {
                script{
                echo 'package hello'
                    echo "packaging the code version ${params.APPVERSION}"
            }
        }
    }
}
            }
