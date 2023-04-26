pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: 'target/*.jar'
                }
            }
        }

        stage('SonarQube analysis') {
            environment {
                SCANNER_HOME = tool 'sonar-scanner'
            }
            steps {
                withSonarQubeEnv('sonarqube-9.9') {
                    sh" ${SCANNER_HOME}/bin/sonar-scanner  \
                    -Dsonar.projectKey=demoproject \
                    -Dsonar.sources=. \
                    -D sonar.host.url=http://18.140.114.114:9000/"
                }
            }
        }
            }
        }
