pipeline {
agent none

stages {
    stage("Cloning") {
	steps {
	    parallel (
		"Slaves 2 Clone": {
		    node("Slave2") {
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
                    node('Slave2') { // I need to reuse Jenkins-node-lin1 here 
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
                    node('Slave2') { // Same story down here
                        sh "mvn test"
                    }
                }
            )
        }
    }
}
}
