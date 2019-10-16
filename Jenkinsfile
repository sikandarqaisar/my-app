
node {
   def sonarUrl = 'sonar.host.url=http://3.19.245.190:9000'
   def mvn = tool (name: 'maven3', type: 'maven') + '/bin/mvn'
   stage('SCM Checkout'){
    // Clone repo
	git branch: 'master', 
    //	credentialsId: 'github', 
	url: 'https://github.com/sikandarqaisar/my-app'
   
   }
   
   stage('Sonar Publish'){
	   withCredentials([string(credentialsId: 'jenkins-id', variable: 'sonarToken')]) {
        def sonarToken = "sonar.login=${sonarToken}"
        sh "${mvn} sonar:sonar -D${sonarUrl}  -D${sonarToken}"
	 }
      
   }
   
	
   stage('Mvn Package'){
	   // Build using maven
	   
	   sh "${mvn} clean package deploy"
   }
   
//   stage('deploy-dev'){
 //      def tomcatDevIp = '172.31.28.172'
//	   def tomcatHome = '/opt/tomcat8/'
//	   def webApps = tomcatHome+'webapps/'
//	   def tomcatStart = "${tomcatHome}bin/startup.sh"
//	   def tomcatStop = "${tomcatHome}bin/shutdown.sh"
	   
//	   sshagent (credentials: ['tomcat-dev']) {
//	      sh "scp -o StrictHostKeyChecking=no target/myweb*.war ec2-user@${tomcatDevIp}:${webApps}myweb.war"
  //        sh "ssh ec2-user@${tomcatDevIp} ${tomcatStop}"
	//	  sh "ssh ec2-user@${tomcatDevIp} ${tomcatStart}"
  //     }
 //  }
   stage('Email Notification'){
		mail bcc: '', body: """Hi Team, You build successfully deployed
		                       Job URL : ${env.JOB_URL}
							   Job Name: ${env.JOB_NAME}
Thanks,
DevOps Team""", cc: '', from: 'sikandar@eurustechnologies.com', replyTo: '', subject: "${env.JOB_NAME} Success", to: 'sikandarqaisar@gmail.com'
   
   }
}
