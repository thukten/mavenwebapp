pipeline {
agent none

stages {
    stage("Cloning") {
	steps {
	    parallel (
		"Slaves 2 Clone": {
		    node("Slave1") {
			git https://github.com/thukten/mavenwebapp.git
		    }
		}
	    )
	}
    }
    stage('Compile') {
        steps {
            parallel (
                "Slave2 Test": {
                    node('Slave1') { // I need to reuse Jenkins-node-lin1 here 
                        sh "mvn compile"
                    }
                }
            )
        }
    }
    stage('Test') {
        steps {
            parallel (
                "Slave2 Deploy": {
                    node('Slave1') { // Same story down here
                        sh "mvn test"
                    }
                }
            )
        }
    }
}
}
