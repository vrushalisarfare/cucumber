node(){

		def repoURL='https://github.com/vrushalisarfare/cucumber.git'

		stage("Prepare Workspace"){
			cleanWs()
			env.WORKSPACE_LOCAL=sh(returnStdout:true,script:'pwd').trim()
			echo"Workspace set to:"+env.WORKSPACE_LOCAL
		}
		stage('Checkout Self'){
		git branch:'master',credentialsId:'',url:repoURL
		}
		stage('Cucumber Tests'){
			withMaven(maven:'maven35'){
				sh """
					cd ${env.WORKSPACE_LOCAL}
					mvn clean test
				"""
			}
		}
		stage('Expose report'){
			archive "**/cucumber.json"
			cucumber '**/cucumber.json'
		}
}
