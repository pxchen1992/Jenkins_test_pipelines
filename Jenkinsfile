/* groovylint-disable LineLength, NestedBlockDepth */
/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any
    tools {
        maven 'maven-3.9.2'
    }

    parameters {
        choice(name: 'VERSION', choices:['1.1.0', '1.2.0', '1.3.0'], description:'')
        booleanParam(name: 'executeTests', defaultValue: true, description:'')
    }

    stages {
        stage('build') {
            steps {
                echo 'building the application... '
                sh 'mvn package'
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
        stage('build image') {
            steps {
                script {
                    echo 'building the docker image...'
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docekr build -t TechScrumDevOps/techscrum:1.0 .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push TechScrumDevOps/techscrum:1.0'
                    }
                }
            }
        }

        stage('deploy') {
            input {
                message 'select the environment to deploy to'
                ok 'DONE'
                parameters {
                    choice(name: 'ENV', choices:['dev', 'staging', 'prod'], description:'')
                }
            }
            steps {
                echo 'deploy the application...'
                echo "deploying version ${params.VERSION}"
                echo "Deploying to ${ENV}"
            }
        }
    }
}