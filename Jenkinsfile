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
                     # URL completa para o binário do Vegeta
                     curl -L https://github.com -o vegeta.tar.gz
                     tar -xvf vegeta.tar.gz
                     chmod +x vegeta
                 fi
                 # Executa o teste (certifique-se que o targets.txt existe no seu GitHub)
                 ./vegeta attack -duration=5s -rate=10 -targets=targets.txt | ./vegeta report
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
