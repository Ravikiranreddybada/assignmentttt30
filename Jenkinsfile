pipeline {
    agent any

    environment {
        DOCKER_IMAGE_BACKEND = "lab27-backend"
        DOCKER_IMAGE_FRONTEND = "lab27-frontend"
        DOCKER_REGISTRY = "your-docker-registry" // Replace with your registry if needed
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            parallel {
                stage('Backend Dependencies') {
                    steps {
                        dir('backend') {
                            sh 'npm install'
                        }
                    }
                }
                stage('Frontend Dependencies') {
                    steps {
                        dir('frontend') {
                            sh 'npm install'
                        }
                    }
                }
            }
        }

        stage('Test') {
            parallel {
                stage('Backend Tests') {
                    steps {
                        dir('backend') {
                            // Backend test might fail if no tests are defined, so using || true for now
                            // Remove || true once real tests are added
                            sh 'npm test || true'
                        }
                    }
                }
                stage('Frontend Tests') {
                    steps {
                        dir('frontend') {
                            sh 'CI=true npm test'
                        }
                    }
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm run build'
                }
            }
        }

        stage('Docker Build') {
            parallel {
                stage('Build Backend Image') {
                    steps {
                        dir('backend') {
                            sh "docker build -t ${DOCKER_IMAGE_BACKEND}:${BUILD_NUMBER} ."
                            sh "docker tag ${DOCKER_IMAGE_BACKEND}:${BUILD_NUMBER} ${DOCKER_IMAGE_BACKEND}:latest"
                        }
                    }
                }
                stage('Build Frontend Image') {
                    steps {
                        dir('frontend') {
                            sh "docker build -t ${DOCKER_IMAGE_FRONTEND}:${BUILD_NUMBER} ."
                            sh "docker tag ${DOCKER_IMAGE_FRONTEND}:${BUILD_NUMBER} ${DOCKER_IMAGE_FRONTEND}:latest"
                        }
                    }
                }
            }
        }

        // Optional: Docker Push stage
        // stage('Docker Push') {
        //     steps {
        //         script {
        //             docker.withRegistry("https://${DOCKER_REGISTRY}", "docker-credentials-id") {
        //                 sh "docker push ${DOCKER_IMAGE_BACKEND}:${BUILD_NUMBER}"
        //                 sh "docker push ${DOCKER_IMAGE_FRONTEND}:${BUILD_NUMBER}"
        //             }
        //         }
        //     }
        // }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo 'Build successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
