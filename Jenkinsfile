pipeline {
    agent any
    stages {
        stage("Clone the project") {
            steps {
                git branch: 'main', url: 'https://github.com/codewiseradvisor/java_simple_hello.git'
            }
        }

        stage("Compilation and Tests") {
            steps {
                sh "./mvnw clean install -DskipTests"
                sh "./mvnw test"
            }
        }

        stage("Tests files") {
            steps {
                sh "ls"
                sh "pwd"
            }
        }

        stage("Stop old containers") {
            steps {
                sh 'docker ps -q | while read -r container_id; do docker stop "$container_id"; done'
            }
        }

        stage("Cleanup old containers") {
            steps {
                sh "docker container prune -f"
            }
        }

        stage("Cleanup old images") {
            steps {
                sh "docker image prune -af"
            }
        }

        stage("Build Docker Image") {
            steps {
                sh "docker build -t my-spring-app ."
            }
        }

        stage("Run Docker Container") {
            steps {
                sh "docker container prune -f"
                sh "sleep 2s"
                sh "docker run -p 8001:8001 -d my-spring-app"
            }
        }
    }
}
