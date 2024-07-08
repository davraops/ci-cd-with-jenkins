pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'http://your-sonarqube-server'
        SONARQUBE_CREDENTIALS = 'sonarqube-credentials-id'
        DOCKER_IMAGE = 'your-docker-image'
        REGISTRY_CREDENTIALS = 'docker-registry-credentials-id'
        REGISTRY_URL = 'your-docker-registry-url'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://your-repository-url.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'mvn clean install'
                }
            }
        }

        stage('Static Code Analysis') {
            steps {
                script {
                    withSonarQubeEnv('SonarQube') {
                        sh 'mvn sonar:sonar -Dsonar.host.url=${env.SONARQUBE_SERVER} -Dsonar.login=${env.SONARQUBE_CREDENTIALS}'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh 'mvn test'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${env.DOCKER_IMAGE}:${env.BUILD_ID} ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry(env.REGISTRY_URL, env.REGISTRY_CREDENTIALS) {
                        docker.image("${env.DOCKER_IMAGE}:${env.BUILD_ID}").push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'kubectl apply -f k8s/deployment.yaml'
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            junit 'target/surefire-reports/*.xml'
        }
        success {
            mail to: 'your-email@example.com',
                 subject: "Jenkins Build ${env.BUILD_ID} Successful",
                 body: "The Jenkins build ${env.BUILD_ID} was successful. The application has been deployed."
        }
        failure {
            mail to: 'your-email@example.com',
                 subject: "Jenkins Build ${env.BUILD_ID} Failed",
                 body: "The Jenkins build ${env.BUILD_ID} has failed. Please check the Jenkins console output for more details."
        }
    }
}
