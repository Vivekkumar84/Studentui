pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Source code checkout successful'
            }
        }

        stage('Build') {
            steps {
                sh '''
                    set -eu
                    mkdir -p dist
                    cp index.html register.html students.html style.css dist/
                    echo "UI build completed"
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    set -eu
                    test -s dist/index.html
                    test -s dist/register.html
                    test -s dist/students.html
                    test -s dist/style.css
                    echo "All required UI files are present"
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    set -eu
                    mkdir -p /var/www/html/studentui
                    cp -r dist/. /var/www/html/studentui/
                    echo "UI deployed successfully"
                '''
            }
        }
    }

    post {
        success {
            echo 'Studentui pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
