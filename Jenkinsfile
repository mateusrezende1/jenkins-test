pipeline {
    agent any  // Define que o pipeline pode rodar em qualquer agente disponível

    environment {
        NODE_VERSION = '20'  // Versão do Node.js que você deseja instalar
        SUDO_PASSWORD = '123456'  // Substitua pela sua senha do sudo
    }

    stages {
        stage('Instalar Homebrew (se necessário)') {
            steps {
                script {
                    echo 'Instalando o Homebrew se necessário...'

                    // Usar sudo para verificar e instalar o Homebrew
                    sh '''
                        echo \$SUDO_PASSWORD | sudo -S command -v brew > /dev/null
                        if [ $? -ne 0 ]; then
                            echo "Homebrew não encontrado. Instalando..."
                            echo \$SUDO_PASSWORD | sudo -S /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
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

                    // Usar sudo para instalar o Node.js
                    sh '''
                        echo \$SUDO_PASSWORD | sudo -S brew install node@${NODE_VERSION}
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
