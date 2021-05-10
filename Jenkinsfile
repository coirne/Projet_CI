pipeline {
    agent any
    stages {
        stage('Clone Git repo') {
        steps {
            git branch: 'main', url: 'https://github.com/coirne/Projet_CI.git'
              }
        }
        
        stage('Test : pytest'){        
        steps {
                sh '''
                    pip3 install -r requirements.txt
                    cd tests
                    pytest
                    cd ..
                '''
          }
        }

    stage('Analyse code : Sonarqube') {
    steps {
    script {
       def scannerHome = tool 'SonarQube Scanner';
           withSonarQubeEnv('SonarQube'){
           sh " ${tool("SonarQube Scanner")}/bin/sonar-scanner \
           -Dsonar.projectKey=Projet_CI \
           -Dsonar.sources=. \
           -Dsonar.css.node=. \
           -Dsonar.host.url=http://172.27.208.1:9000 \
           -Dsonar.login=754fee56c1f8a22d2e88cbadf675a212d7fa68fb"
               }
    }
           }
    }
    
        stage('Store Artefact : nexus'){        
        steps {
                sh '''
                    tar -czf archive$BUILD_NUMBER.tar.gz /var/jenkins_home/workspace/Projet_CI_pipeline
                    curl -v -u admin:corine --upload-file /var/jenkins_home/workspace/archive$BUILD_NUMBER.tar.gz  http://172.27.208.1:8081/repository/projet_final/
                '''
          }

    }
}  
}
