pipeline {
    agent any

    environment {
        IMAGE_NAME = "us-central1-docker.pkg.dev/clever-axe-447305-k1/sample-images-repo/simple-webapp"
        TAG = "latest"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/shar1810/Simple-Webapp.git', branch: 'main'
            }
        }

        stage('Code Scan (Placeholder)') {
            steps {
                echo "Running basic code scan (placeholder)..."
                sh 'ls -la && cat app.py || echo "app.py not found"'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t \$IMAGE_NAME:\$TAG ."
                }
            }
        }

        stage('Image Scan (Placeholder)') {
            steps {
                echo "Image scanning with Trivy or other tools can be done here"
            }
        }

        stage('Push to Artifact Registry') {
            steps {
                script {
                    sh "docker push \$IMAGE_NAME:\$TAG"
                }
            }
        }

        stage('Deploy Locally') {
            steps {
                script {
                    // Stop old container if exists
                    sh "docker rm -f simple-webapp || true"
                    // Run new container
                    sh "docker run -d -p 82:5000 --name simple-webapp \$IMAGE_NAME:\$TAG"
                }
            }
        }
    }
}
