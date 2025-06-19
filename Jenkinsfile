pipeline {
    agent any  // 使用任意可用节点

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // 拉取 GitHub 代码
            }
        }

        stage('Setup Python') {
            steps {
                sh 'python3 --version'  // 检查 Python 环境
                // 可选：安装依赖（如 pip install -r requirements.txt）
            }
        }

        stage('Run Python Script') {
            steps {
                sh 'python3 get_AAD_graph_flow-and-response_time.py'  // 运行 Python 文件
            }
        }
    }
}
