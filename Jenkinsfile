pipeline {
agent none

stages {
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
