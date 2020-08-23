pipeline {
agent none

stages {
    stage('Clone') {
        steps {
            parallel (
                "Slave1 Clone": {
                    node('Slave1') { 
                        git 'https://github.com/thukten/mavenwebapp.git'
                    }
                },
                "Slave2 Clone": {
                    node('Slave2') { 
                        git 'https://github.com/thukten/mavenwebapp.git'
                    }
                }
            )
        }
    }
    stage('Compile') {
        steps {
            parallel (
                "Slave1 Compile": {
                    node('Slave1') { // I need to reuse Jenkins-node-lin1 here 
                        sh "mvn compile"
                    }
                },
                "Slave2 Compile": {
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
                "Slave1 Test": {
                    node('Slave1') { // Same story down here
                        sh "mvn test"
                    }
                },
                "Slave2 Test": {
                    node('Slave2') { // Same story down here
                        sh "mvn test"
                    }
                }
            )
        }
    }
}
}
