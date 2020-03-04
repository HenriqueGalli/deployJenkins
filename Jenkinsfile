pipeline {
    agent any

    triggers {
        git url :'https://github.com/lucas-atomic/maven-project.git'
        pollSCM('* * * * *')
    }

    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deployments'){
            parallel {
                stage ('Deploy to Staging'){
                    steps {
                        sh  'mvn deploy package'
                        
                    }
                }
            }
        }        
    }
}
