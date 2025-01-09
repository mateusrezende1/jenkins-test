pipeline {
    agent any  // Define que o pipeline pode rodar em qualquer agente disponível

    environment {
        NODE_VERSION = '20'  // A versão do Node.js que você deseja instalar
        CYPRESS_VERSION = '13.0.0'  // Versão do Cypress (alterar conforme necessário)
    }

    stages {
        stage('Preparar Ambiente') {
            steps {
                script {
                    echo 'Instalando Node.js...'

                    // Instalar o Node.js usando o NVM (Node Version Manager)
                    sh '''
                        curl -sL https://deb.nodesource.com/setup_${NODE_VERSION}.x | sudo -E bash -
                        sudo apt-get install -y nodejs
                    '''
                    
                    // Verifique se o Node.js foi instalado corretamente
                    sh 'node -v'
                    sh 'npm -v'
                }
            }
        }

        stage('Instalar Dependências') {
            steps {
                script {
                    echo 'Instalando dependências do Node.js...'
                    
                    // Instalar dependências do projeto
                    sh 'npm install'  // Instala o Cypress e outras dependências listadas no package.json
                }
            }
        }

        stage('Instalar Cypress') {
            steps {
                script {
                    echo "Instalando o Cypress versão ${CYPRESS_VERSION}..."
           
                }
            }
        }

    }