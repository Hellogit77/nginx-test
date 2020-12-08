pipeline {
    agent {
        label "generic"
    }
    stages {
        stage("Create docker image for testing") {
            steps {
                sh """
                    python3 -m molecule create
                """
            }
        }
        stage("Apply ansible role to docker image") {
            steps {
                sh """
                    python3 -m molecule converge
                """
            }
        }
        stage("Check Idempotency") {
            steps {
                sh """
                    python3 -m molecule idempotence
                """
            }
        }
        stage("Cleanup molecule") {
            steps {
                sh """
                    python3 -m molecule cleanup
                """
            }
        }
        stage("Destroy molecule instance") {
            steps {
                sh """
                    pyhton -m molecule destroy
                """
            }
        }
    }
}