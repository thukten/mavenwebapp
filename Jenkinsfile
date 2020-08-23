pipeline {
agent none

stages {
    stage('Compile') {
        steps {
            parallel (
                "Slave1 Test": {
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
                "Slave1 Deploy": {
                    node('Slave1') { // Same story down here
                        sh "mvn test"
                    }
                }
            )
        }
    }
}
}
