pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    parameters{
        choice(name: 'VERSION', choice:['1.1.0', '1.2.0', '1.3.0'], description:'')
        booleanParam(name: 'executeTests', defaultValue: true, description:'')

    }
    environment {
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials('server-credentials')

    }

    stages {
        stage('build') {
            steps {
                echo 'building the application... '
                sh "mvn install"
            }
        }
      
        stage('test') {
            when{
                expression{
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
                sh "deploying version ${params.VERSION}"
                withCredentials([
                    usernamePassword(credentials: 'server-credentials', usernameVariable: USER, passwordVariable: PWD)
                ]) {
                    sh " some script ${USER} ${PWD}"
                }
            }
        }
        post{
            always{
                //sending an email out to the team about the bill condition
            }
            success{
                //only relevant if the build succeeded 
            }
            failure{
                //all the different conditions on the past block
            }
        
        }
    }
}s