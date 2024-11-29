pipeline {
    agent any

    environment {
        PYTHON_ENV = 'venv'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/mindeng88/helloworld.git'
            }
        }

        stage('Setup Python') {
            steps {
                script {
                    sh 'python3 -m venv $PYTHON_ENV'
                    sh '. $PYTHON_ENV/bin/activate && pip install -r requirements.txt'
                }
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                // 启动 Flask 服务并输出日志
                sh '. $PYTHON_ENV/bin/activate && export FLASK_APP=app.py && flask run --host=0.0.0.0 --port=5000 > app.log 2>&1 &'
            }
        }

        stage('List Files') {
            steps {
                sh 'ls -al'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'deactivate || true'
        }
    }
}
