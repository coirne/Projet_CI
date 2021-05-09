// Powered by Infostretch 

timestamps {

node () {

	stage ('Projet_CI_no_pipeline - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github_id', url: 'https://github.com/coirne/Projet_CI.git']]]) 
	}
	stage ('Projet_CI_no_pipeline - Build') {
 	
withEnv(["JAVA_HOME=${ tool '"+JDK+"' }", "PATH=${env.JAVA_HOME}/bin"]) { 

// Unable to convert a build step referring to "jenkins.plugins.shiningpanda.builders.PythonBuilder". Please verify and convert manually if required.
// Unable to convert a build step referring to "hudson.plugins.sonar.SonarRunnerBuilder". Please verify and convert manually if required.		// Shell build step
sh """ 
rm -f /var/jenkins_home/workspace/*.tar.gz
tar -cf /var/jenkins_home/workspace/archive_version$BUILD_NUMBER.tar.gz /var/jenkins_home/workspace/Projet_CI_no_pipeline
ls /var/jenkins_home/workspace/
curl -v -u admin:corine --upload-file /var/jenkins_home/workspace/archive_version$BUILD_NUMBER.tar.gz  http://172.27.208.1:8081/repository/projet_final/ 
 """ 
	}
}
}
}