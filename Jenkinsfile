pipeline {
    agent any

    // **NUEVO BLOQUE: CONFIGURACIÓN DEL JDK 21**
    tools {
        // Le dice a Jenkins que use el JDK llamado 'JDK_21_LOCAL' que configuraste
        jdk 'JDK_21_LOCAL'
    }

    stages {
        stage('Clonar el Repositorio') {
            steps {
                git branch: 'origin/main', url: 'https://github.com/XxTheTianxX/MICRO-BALANCEO'
            }
        }
        stage('Construir imagen de Docker') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'MONGO_URI', variable: 'MONGO_URI')]) {
                        docker.build("proyectos-micro-v1", "--build-arg MONGO_URI=${MONGO_URI} .")
                    }
                }
            }
        }
        stage('Desplegar contenedores Docker') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'MONGO_URI', variable: 'MONGO_URI')]) {
                        sh 'docker-compose up -d'
                    }
                }
            }
        }
    }
    
    post {
        always {
            emailext (
                // ... (el contenido de tu post-build)
            )
        }
    }
}
                


