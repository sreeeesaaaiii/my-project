pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        S3_BUCKET = 'sai232'
    }

    stages {

        stage('Deploy to S3') {
            steps {
                sh '''
                    echo "Checking AWS..."
                    aws sts get-caller-identity

                    echo "Deploying files..."
                    aws s3 sync . s3://$S3_BUCKET \
                        --region $AWS_REGION \
                        --delete \
                        --exclude ".git/*" \
                        --exclude "Jenkinsfile"

                    echo "Deployment completed!"
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment to S3 completed successfully!'
        }

        failure {
            echo '❌ S3 deployment failed.'
        }
    }
}
