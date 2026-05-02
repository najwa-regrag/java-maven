pipeline {
    triggers {
        pollSCM('H/2 * * * *')
    }
    agent {
        docker {
            image 'my-maven-git:latest'
            args '-v $HOME/.m2:/root/.m2'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                deleteDir()
                git url:'https://github.com/najwa-regrag/java-maven.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                script {
                    echo "Début de la compilation..."
                    dir("maven") {
                        sh 'mvn clean test package'
                        sh "java -jar target/*.jar"
                    }
                }
            }
        }
    }
}
