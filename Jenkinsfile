pipeline {
    agent any

    tools {
        maven "MAVEN_HOME"
    }
    
    parameters { choice(name: 'browser', choices: [' ', 'chrome', 'firefox', 'edge', 'ie', 'safari'], description: '') }

    stages {
    	stage('setup') {
            steps {
                browserstack(credentialsId: '8ca7f885-b257-4389-8820-421e6ea983f1') {
                echo "inside browser stack"
                browserStackReportPublisher 'automate'
                }
            }
           }
        stage('Build') {
            steps {
                git 'https://github.com/gullapallichaitanya/SampleProject003.git'
                echo "Browser: ${params.browser}"
                bat 'mvn -Dmaven.test.failure.ignore=true clean test ${params.browser}'
            }

            post {
                success {
                    junit '**/ExtentReport/sparkReport_*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
