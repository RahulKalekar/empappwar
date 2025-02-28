pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "localmvn"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/RahulKalekar/empappwar.git'

                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                 bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/empapp.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
           steps{
              deploy adapters: [tomcat9(credentialsId: '5e98a579-f436-492c-b044-ea3f5557a8a2', path: '', url: 'http://localhost:8080/')], contextPath: '/empapp', war: '**/*.war'
            }
           //Here i gave credentialsId of global which is admin admin
        }
    }
}
