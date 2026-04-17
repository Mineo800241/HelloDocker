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
                    curl -L "https://github.com/tsenart/vegeta/releases/download/v12.8.4/vegeta_12.8.4_linux_amd64.tar.gz" -o vegeta.tar.gz
                    tar -xvf vegeta.tar.gz
                    chmod +x vegeta
                    fi
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
