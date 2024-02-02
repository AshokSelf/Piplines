pipeline {
    agent any

    stages {
        stage('Git Clone') {
            steps {
                git 'https://github.com/Ashokkunchala/myweb.git'
            }
        }
        stage('MVN Compile') {
            steps {
                sh 'mvn compile'
            }
        }
         stage('MVN test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('MVN Clean Package') {
            steps {
                sh 'mvn clean package'
                sh '''mvn sonar:sonar -Dsonar.url=http://localhost:9000 -Dsonar.login=squ_adccf0cc9dd91f6163b31470ae479cb7bad4b482 -Dsonar.projectName=Petclinic \
                -Dsonar.java.binaries=. \
                -Dsonar.projectKey=Petclinic '''
                
            }
        }
    }
    post {
            always {
                emailext (
                    subject: "Pipeline Status: ${BUILD_NUMBER}",
                    body: '''<html>
                                <body>
                                    <p>Build Status: ${BUILD_STATUS}</p>
                                    <p>Build Number: ${BUILD_NUMBER}</p>
                                    <p>Check the <a href="${BUILD_URL}">console output</a>.</p>
                                </body>
                            </html>''',
                    to: 'ashokkunchla@gmail.com',
                    from: 'jenkins@example.com',
                    replyTo: 'jenkins@example.com',
                    mimeType: 'text/html'
                )
            }
        }
}
