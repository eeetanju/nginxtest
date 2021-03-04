pipeline {
 agent none
  options {
    timeout(time: 1, unit: 'MINUTES') 
  }
  stages {
    stage('preamble') {
        steps {
            script {
                openshift.withCluster() {
                    openshift.withProject("myproject-uat") {
                        echo "Using project: ${openshift.project()}"
                    }
                }
            }
        }
    }
	
	stage('preamble') {
        steps {
            script {
                openshift.withCluster() {
                    openshift.withProject("myproject-uat") {
                        openshift.apply("-f buildConfig.yaml")
                    }
                }
            }
        }
    }
  }
}
