pipeline {
    agent any
    environment {
        CYPRESS_CACHE_FOLDER = "${WORKSPACE}/.cache/Cypress"
    }
    stages {
        stage('Preparar Ambiente') {
            steps {
                script {
                    if (!fileExists('node_modules')) {
                        echo 'Instalando dependências...'
                        sh 'npm install'
                    }
                }
            }
        }

        stage('Executar Cypress Tests') {
            steps {
                script {
                    echo 'Rodando testes Cypress...'
                    sh 'npx cypress run'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finalizado.'
        }

        success {
            echo 'Testes concluídos com sucesso.'
        }

        failure {
            echo 'Testes falharam. Verifique os relatórios para mais detalhes.'
        }
    }
}
