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
                withSonarQubeEnv('jenkins-sonar') {
                    sh" ${SCANNER_HOME}/bin/sonar-scanner \
                    -Dsonar.sources=. "
                }
            }
        }
            }
        }
