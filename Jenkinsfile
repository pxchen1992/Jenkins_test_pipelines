pipeline {
    agent any
    parameters{
        choice(name: 'VERSION', choice:['1.1.0', '1.2.0', '1.3.0'], description:'')
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