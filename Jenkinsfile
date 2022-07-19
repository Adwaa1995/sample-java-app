pipeline {

    agent any

    stages {

        stage('Build'){
            steps {
                sh "mvn clean"

                sh "mvn compile"
            }
        }

        stage('Test'){
            steps {
                sh "mvn test"
            }

            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }

        stage('sonar scan'){
            steps {
              sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=Adwaa-alhosyani \
  -Dsonar.host.url=http://54.226.50.200 \
  -Dsonar.login=sqp_9018bd54b4334a14753007717ba3052efb14f09b"
            }
        }

        stage('Package'){
            steps {
                
                sh "mvn package"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
                }
            }
        }

    }

}