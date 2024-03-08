pipeline {
    agent any
    stages {
        stage("Clone the project") {
            steps {
                git branch: 'main', url: 'https://github.com/codewiser116/java_simple_app'
            }
        }

        stage("Tests files") {
            steps {
                sh "ls"
                sh "pwd"
            }
        }

        stage('Checkout Tests') {
            steps {
                // Checkout test code repository
                dir('tests') {
                    git(url: 'https://github.com/codewiser116/jdbc_automation', branch: 'main')
                }
            }
        }
        stage('Run Tests') {
            steps {
                // Navigate into the tests directory and run tests
                dir('tests') {
                    echo 'Running tests...'
                    sh "./mvnw test"
                }
            }
        }
    }
}
