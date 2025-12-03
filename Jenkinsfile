pipeline {
    agent any
    
    triggers {
        githubPush()
    }

    tools {
        maven 'M2_HOME'
    }

    stages {
        stage("GIT") {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AbdessettarBenHassen/BenHassen_Abdessettar_4Sleam1.git',
                    credentialsId: 'Github_pat'
            }
        }

        stage('Maven Compile') {
            steps {
                sh "mvn compile -DskipTests"
            }
        }

        stage('Maven Clean') {
            steps {
                sh "mvn clean"
            }
        }

        stage('Maven Package') {
            steps {
                sh "mvn package -DskipTests"
            }
        }

    }
}