pipeline {
    agent any // Executa em qualquer worker disponível

    stages {
        stage('Checkout') {
            steps {
                // Baixa o código do repositório configurado no job
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Compilando o projeto...'
                // Exemplo para Node.js ou Java:
                // sh 'npm install && npm run build'
                // sh './gradlew build'
            }
        }

        stage('Test') {
            steps {
                echo 'Executando testes unitários...'
                // sh 'npm test' ou sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Fazendo deploy para o ambiente de Staging...'
                // Exemplo: comando para copiar arquivos ou atualizar container
                // sh './deploy.sh'
            }
        }
    }

    post {
        success {
            echo 'Pipeline finalizado com sucesso!'
        }
        failure {
            echo 'Ocorreu um erro no pipeline. Verifique os logs.'
        }
    }
}
