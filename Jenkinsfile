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
						openshift.apply("-f imageStream.yaml")
                    }
                }
            }
        }
    }
	
	stage('build') {
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
	
	stage('deploy') {
        steps {
            script {
                openshift.withCluster() {
                    openshift.withProject("myproject-uat") {
                        openshift.apply("-f deploymentConfig.yaml")
                    }
                }
            }
        }
    }
	
	stage('svc-route') {
        steps {
            script {
                openshift.withCluster() {
                    openshift.withProject("myproject-uat") {
                        openshift.apply("-f service.yaml")
						openshift.apply("-f route.yaml")
                    }
                }
            }
        }
    }
	
  }
}
