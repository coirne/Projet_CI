pipeline {
    agent any
    stages {
        stage('Clone Git repo') {
        steps {
            git branch: 'main', url: 'https://github.com/coirne/Projet_CI.git'
              }
        }
        
        stage('Test'){        
        steps {
                sh 
                '''
                    pip3 install -r requirements.txt
                    ./tests
                    pytest
                    cd ..
                '''
          }
        }

        stage('Code quality'){  
            withCredentials([[credentialsId: 'sonar_id']]) {
            withSonarQubeEnv('SonarQube') {    
                mvn "-Dsonar.projectKey=projet_final -Dsonar.sources=."
                }
            }
          }

        stage('Store Artefact'){        
        steps {
                sh 
                '''
                    rm -f /var/jenkins_home/workspace/*.tar.gz
                    tar -cf /var/jenkins_home/workspace/archive$BUILD_NUMBER.tar.gz /var/jenkins_home/workspace/Projet_CI
                    ls /var/jenkins_home/workspace/
                    curl -v -u admin:corine --upload-file /var/jenkins_home/workspace/archive$BUILD_NUMBER.tar.gz  http://172.27.208.1:8081/repository/projet_final/'
                '''
          }

    }
}  
}
