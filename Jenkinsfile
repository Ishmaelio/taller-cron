pipeline {
    agent any
    triggers {
        cron('*/5 * * * *')   // ejecuta cada 5 minutos
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Compilar') {
            steps {
                bat 'javac HolaMundo.java'
            }
        }
        stage('Desplegar') {
            steps {
                bat '''
                if not exist despliegue mkdir despliegue
                copy HolaMundo.class despliegue
                '''
            }
        }
        stage('Ejecutar') {
            steps {
                bat 'java -cp despliegue HolaMundo > despliegue\\salida.txt'
                bat 'echo Ejecución finalizada'
            }
        }
    }
    post {
	success {
		archiveArtifacts artifacts: 'despliegue/**', fingerprint: true
	}
    }
}