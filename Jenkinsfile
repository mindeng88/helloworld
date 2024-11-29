pipeline {
    agent any

    environment {
        PYTHON_ENV = 'venv'
    }

    stages {
        stage('Checkout') {
            steps {
                // 从 GitHub 仓库检出代码
                git 'https://github.com/mindeng88/helloworld.git'
            }
        }

        stage('Setup Python') {
            steps {
                script {
                    // 创建虚拟环境并安装依赖
                    sh 'python3 -m venv $PYTHON_ENV'
                    sh '. $PYTHON_ENV/bin/activate && pip install -r requirements.txt'
                }
            }
        }

        stage('Run Tests') {
            steps {
                // 运行测试（这里可以添加实际的测试步骤）
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                // 启动 Flask 服务
                sh '. $PYTHON_ENV/bin/activate && python app.py &'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // 可选：停止 Flask 服务并清理虚拟环境
            sh 'deactivate || true'
        }
    }
}
