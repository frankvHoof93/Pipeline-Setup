pipeline {
    agent any
    stages {
        stage('Non-Parallel Stage') {
            steps {
                echo 'This stage will be executed first.'
                checkout scm
                stash 'source'
            }
        }
        stage('Parallel Stage') {
            parallel {
                stage('Branch A') {
                    agent any
                    steps {
                        unstash 'source'
                        echo "On Branch A"
                    }
                }
                stage('Branch B') {
                    agent any
                    steps {
                        unstash 'source'
                        echo "On Branch B"
                    }
                }
                stage('Branch C') {
                    agent any
                    stages {
                        stage('Nested 1') {
                            steps {
                                unstash 'source'
                                echo "In stage Nested 1 within Branch C"
                            }
                        }
                        stage('Nested 2') {
                            steps {
                                unstash 'source'
                                echo "In stage Nested 2 within Branch C"
                            }
                        }
                    }
                }
            }
        }
        stage('Final Stage') {
            steps {
                echo 'This stage will be executed last.'
            }
        }
    }
}
