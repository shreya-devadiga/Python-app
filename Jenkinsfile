pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t python-app:1.0 .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker run --rm python-app:1.0 python -c "import app; print(\"Test passed\")"'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f python-app1 || true
                    docker run -d \
                        --name python-app1 \
                        -p 8081:5000 \
                        python-app:1.0
                '''
            }
        }
    }
}
