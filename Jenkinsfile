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
                // 使用 withCredentials 指令将凭证注入到环境变量
                withCredentials([
                    // 绑定用户名密码凭证到两个环境变量：MY_USERNAME 和 MY_PASSWORD
                    string(
                        credentialsId: 'SP-API-TK',
                        variable: 'ORCH_TOKEN' // 自定义密钥环境变量名
                    ),
                    string(
                        credentialsId: 'Jenkins_webhook',
                        variable: 'TEAMS_WEBHOOK' // 自定义密钥环境变量名
                    ),
                    string(
                        credentialsId: 'ORCH_HOST',
                        variable: 'ORCH_HOST' // 自定义密钥环境变量名
                    )
                ]) {
                    // 在这个块内的所有步骤都可以访问到上面定义的环境变量
                    echo "API Token is $ORCH_TOKEN"
                    // 执行你的 Python 脚本
                    sh 'python3 get_AAD_graph_flow-and-response_time.py'  // 运行 Python 文件
                }               
            }
        }
    }
}
