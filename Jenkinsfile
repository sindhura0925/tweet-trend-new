pipeline {
    agent {
        node {
            label "maven"
        }
    }

    environment {
        PATH = "/opt/apache-maven-3.9.5/bin:$PATH"
    }

    stages {
        stage('build') {
            steps {
                echo "--------------BUILD STARTED------------------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "--------------BUILD STARTED------------------"
            }
          
        }

        stage('test')
        {
            steps {
                echo "--------------UNIT TEST STARTED------------------"
                sh 'mvn surefire-report:report'
                echo "--------------UNIT TEST COMPLETED------------------"
            }
        }

        stage('SonarQube analysis') {
            environment
            {
                scannerHome = tool 'valaxy-sonar-scanner';
            }
            steps
            {
                withSonarQubeEnv('valaxy-sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
                sh "${scannerHome}/bin/sonar-scanner"
            }
            
            }
  }
    }
}

