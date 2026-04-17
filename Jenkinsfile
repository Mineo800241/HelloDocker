pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Compilando o projeto...'
                // sh 'mvn clean install' // Descomente se for usar Maven
            }
        }

        stage('Stress Test') {
            steps {
                echo 'Iniciando ataque de estresse...'
                sh '''
                    # Baixa o Vegeta se não existir
                    if [ ! -f vegeta ]; then
                        wget https://github.com
                        tar -zxvf vegeta_12.8.4_linux_amd64.tar.gz
                    fi

                    # Executa o ataque (ajustado para 200 req/s para não travar seu PC de cara)
                    echo "GET http://localhost:8080/" | ./vegeta attack -rate=200 -duration=30s | ./vegeta report
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Fazendo deploy...'
            }
        }
    }

    post {
        success {
            echo 'Pipeline finalizado com sucesso!'
        }
        failure {
            echo 'Ocorreu um erro. Verifique os logs no Console Output.'
        }
    }
}
