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
                if [ ! -f vegeta ]; then
                        # O curl baixa o arquivo; o -L segue redirecionamentos e o -o define o nome do arquivo
                        curl -L https://github.com -o vegeta.tar.gz
                        tar -xvf vegeta.tar.gz
                        chmod +x vegeta
                    fi
                    ./vegeta attack -duration=5s -rate=10 -targets=targets.txt |
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
