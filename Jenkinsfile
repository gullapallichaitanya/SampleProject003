pipeline {
    agent any

    tools {
        maven "MAVEN_HOME"
    }

    stages {
    	stage('setup') {
            steps {
                browserstack(credentialsId: '8ca7f885-b257-4389-8820-421e6ea983f1')
            }
           }
        stage('Build') {
            steps {
                git 'https://github.com/gullapallichaitanya/SampleProject002.git'

                bat "mvn -Dmaven.test.failure.ignore=true clean test"
            }

            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
