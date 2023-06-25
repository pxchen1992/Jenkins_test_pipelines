/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any

    parameters {
        choices(name: 'VERSION', choice:['1.1.0', '1.2.0', '1.3.0'], description:'')
        booleanParam(name: 'executeTests', defaultValue: true, description:'')
    }
}

    stages {
        stage('build') {
            steps {
                echo 'building the application... '
            }
        }

        stage('test') {
            when {
                expression {
                    params.executeTests == true
                }
            }
            steps {
                echo 'testing the application...'
            }
        }

        stage('deploy') {
            steps {
                echo 'deploy the application...'
                echo "deploying version ${params.VERSION}"
            }
        }
    }
