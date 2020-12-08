pipeline {
    agent {
        label "generic"
    }
    stages {
        stage("Create docker image for testing") {
            steps {
                sh """
                    molecule create
                """
            }
        }
        stage("Apply ansible role to docker image") {
            steps {
                sh """
                    molecule converge
                """
            }
        }
        stage("Check Idempotency") {
            steps {
                sh """
                    molecule idempotence
                """
            }
        }
        stage("Cleanup molecule") {
            steps {
                sh """
                    molecule cleanup
                """
            }
        }
        stage("Destroy molecule instance") {
            steps {
                sh """
                    molecule destroy
                """
            }
        }
    }
}