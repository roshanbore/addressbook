pipeline {
    agent any
    parameters {
         string(name: 'rosh', defaultValue: 'test', description: 'env to compile') }

    stages {
        stage('compile') {
            steps {
                echo 'compile hello'
                echo "compile in rosh: ${params.rosh}" 
            }
        }
        stage('unit test') {
            steps {
                echo 'unittest hello'
            }
        }
        stage('package') {
            steps {
                echo 'package hello'
            }
        }
    }
}
