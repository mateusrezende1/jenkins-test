pipeline {
    agent any

    environment {
        NODE_VERSION = '16'  // A versão do Node.js que você deseja instalar
        SUDO_PASSWORD = '123456'  // Defina a senha do sudo
    }

    stages {
        stage('Instalar Node.js') {
            steps {
                script {
                    echo 'Instalando Node.js...'

                    // Enviar a senha para o sudo usando o comando 'echo' e o 'sudo -S'
                    sh """
                        echo \$SUDO_PASSWORD | sudo -S curl -sL https://deb.nodesource.com/setup_\${NODE_VERSION}.x | bash -
                        echo \$SUDO_PASSWORD | sudo -S apt install -y nodejs
                    """
                }
            }
        }
    }
}
