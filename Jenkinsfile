pipeline {
    agent any
    
    stages {
        stage ('SCM Checkout'){
            steps {
                git(branch: 'main', url: 'https://github.com/vagile-devsecops/p1-basic.git', credentialsId: 'vagile-devsecops')
            }
        }
        stage ('mvn package') {
            steps {
                bat 'mvn clean package'
            }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh """
                        mvn sonar:sonar \
                        -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
                        -Dsonar.projectName='Vagile WebApp' \
                        -Dsonar.java.binaries=target/classes
                    """
                }
            }
        }
        
        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
            
        }
        stage ('tomcat-deployment'){
            steps {
                bat 'mvn tomcat7:deploy'
            }
        
         }
     }
     post {
         failure {
             slackSend(
                 color: "red",
                 channel: "devsecops",
                 message: ":fire: *FAILED* have a look into it :male-detective:")
         }
          success {
             slackSend(
                 color: "green",
                 channel: "devsecops",
                 message: " *passed*:"
                 )
         }
     }
}
