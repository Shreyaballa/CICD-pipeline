pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/html"
        CLONE_DIR  = "app"
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo '📥 Cloning GitHub repo using credentials'
                sh '''
                    rm -rf $CLONE_DIR
                    git clone https://github.com/Shreyaballa/CICD-pipeline.git $CLONE_DIR
                '''
            }
        }

        stage('Deploy to Apache') {
            steps {
                echo '🚀 Deploying to Apache web server'
                sh '''
                    sudo rm -rf $DEPLOY_DIR/*
                    sudo cp -r $CLONE_DIR/index.php $DEPLOY_DIR/
                    sudo chown -R www-data:www-data $DEPLOY_DIR
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment Successful!'
        }
        failure {
            echo '❌ Deployment Failed!'
        }
    }
}
