def slave1_node
def slave2_node

pipeline {
    agent none

    stages {
        stage('Build') {
            steps {
            parallel (
                "Slave1 Build": {
                    node('Salve1') {
                        slave1_node = env.Slave1
                    }
                },
                "Slave2 Build": {
                    node('Slave2') {
                        slave2_node = env.Slave2
                    }
                }
            )
            }
        }
        stage('Test') {
            steps {
                parallel (
                    "Slave1 Test": {
                        node(slave1_node) {
                            sh "mvn compile"
                        }
                    },
                    "Slave2 Test": {
                        node(slave2_node) {
                            sh "mvn compile"
                        }
                    }
                )
            }
        }
        stage('Deploy') {
            steps {
                parallel (
                    "Slave1 Deploy": {
                        node(slave1_node) {
                            sh "mvn test"
                        }
                    },
                    "Slave2 Deploy": {
                        node(slave2_node) {
                            sh "mvn test"
			}
                    }
                )
            }
        }
    } // End stages
}
