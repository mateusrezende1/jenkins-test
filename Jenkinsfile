pipeline {
    agent any  // Define que o pipeline pode rodar em qualquer agente disponível

    environment {
        NODE_VERSION = '20'  // Defina a versão do Node.js que você deseja instalar
    }

    stages {
        stage('Instalar Homebrew (se necessário)') {
            steps {
                script {
                    echo 'Instalando o Homebrew se necessário...'

                    // Verifica se o Homebrew está instalado e instala, se necessário
                    sh '''
                        if ! command -v brew &> /dev/null; then
                            echo "Homebrew não encontrado. Instalando..."
                            /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
                        else
                            echo "Homebrew já está instalado."
                        fi
                    '''
                }
            }
        }

        stage('Instalar Node.js') {
            steps {
                script {
                    echo 'Instalando o Node.js com Homebrew...'

                    // Instalar o Node.js com o Homebrew
                    sh '''
                        brew install node@${NODE_VERSION}
                    '''
                    
                    // Verificar se a instalação foi bem-sucedida
                    sh 'node -v'
                    sh 'npm -v'
                }
            }
        }

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
