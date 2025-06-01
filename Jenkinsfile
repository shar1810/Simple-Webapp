pipeline {
    agent any

    environment {
        IMAGE_NAME = "us-central1-docker.pkg.dev/clever-axe-447305-k1/sample-images-repo/simple-webapp"
        TAG = "latest"
    }

    stages {

        stage('Code Scan (Placeholder)') {
            steps {
                echo "Running basic code scan (placeholder)..."
                sh 'ls -la && cat index.html || echo "index.html not found"'
            }
        }

        stage('Authenticate GCP') {
            steps {
                withCredentials([file(credentialsId: 'gcp-service-account-json', variable: 'SERVICE_ACCOUNT_KEY')]) {
                    sh '''
                        gcloud auth activate-service-account --key-file=$SERVICE_ACCOUNT_KEY
                        gcloud auth configure-docker us-central1-docker.pkg.dev
                    '''
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME:$TAG ."
            }
        }

        stage('Image Scan (Placeholder)') {
            steps {
                echo "Image scanning with Trivy or other tools can be done here"
            }
        }

        stage('Push to Artifact Registry') {
            steps {
                sh "docker push $IMAGE_NAME:$TAG"
            }
        }

        stage('Deploy Locally') {
            steps {
                sh '''
                    docker rm -f simple-webapp || true
                    docker run -d -p 82:80 --name simple-webapp $IMAGE_NAME:$TAG
                '''
            }
        }
    }
}
