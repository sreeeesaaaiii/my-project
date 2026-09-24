pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        S3_BUCKET  = 'sai232'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/sreeeesaaaiii/my-project.git'
            }
        }

        stage('Deploy to S3') {
            steps {
                sh '''
                    aws s3 sync . s3://$S3_BUCKET \
                    --region $AWS_REGION \
                    --delete \
                    --exclude ".git/*" \
                    --exclude "Jenkinsfile"
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment to S3 completed successfully!'
        }

        failure {
            echo 'S3 deployment failed.'
        }
    }
}
