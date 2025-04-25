node(){

	
	stage('Code Checkout'){
		checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[ url: 'https://github.com/Nithin2751/MavenBuild.git']])
	}
	stage('Build Automation'){
		sh """
			ls -lart
			mvn clean install
			ls -lart target

		"""
	}
	
	
	stage('Code Coverage ') {
	    //sh "curl -o coverage.json 'http://35.154.151.174:9000/sonar/api/measures/component?componentKey=com.java.example:java-example&metricKeys=coverage';sonarCoverage=`jq '.component.measures[].value' coverage.json`;if [ 1 -eq '\$(echo '\${sonarCoverage} >= 50'| bc)' ]; then echo 'Failed' ;exit 1;else echo 'Passed'; fi"
	}
	
	stage('Code Deployment'){
		deploy adapters: [tomcat10(credentialsId: 'TomcatCreds', path: '', url: 'http://http://54.167.173.84:8080///')], contextPath: 'Planview', onFailure: false, war: 'target/*.war'
	}
}
