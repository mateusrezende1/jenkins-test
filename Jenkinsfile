pipeline {
    agent any  // Define que o pipeline pode rodar em qualquer agente disponível

    stages {
        stage('Instalar Dependências do Projeto') {
            steps {
                script {
                    echo 'Instalando dependências do projeto...'
                    // Instalar as dependências do projeto (se houver package.json)
                    sh 'npm install'
                }
            }
        }

        stage('Executar Testes Cypress') {
            steps {
                script {
                    echo 'Executando os testes com Cypress...'
                    // Executa os testes Cypress (se o Cypress estiver configurado no projeto)
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
            echo 'Pipeline executado com sucesso!'
        }

        failure {
            echo 'Pipeline falhou. Verifique os logs para mais detalhes.'
        }
    }
}
