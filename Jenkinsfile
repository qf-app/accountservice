pipeline {
    agent any

    tools {
       
        maven "M3"
    }

    stages {
        stage('prepare') {
          steps {
               echo "hello world"
          }
        }
        stage('Build') {
            steps {
                
               git branch: 'main', url: 'https://github.com/qf-app/accountservice.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true -s settings.xml clean deploy"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
