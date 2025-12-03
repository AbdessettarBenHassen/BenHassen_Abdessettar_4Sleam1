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

        stage('Test Docker') {
            steps {
                sh 'docker version'
                sh 'docker ps'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t abdessettarenhassen/student-management:latest .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_creds', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push abdessettarenhassen/student-management:latest'
                }
            }
        }
    }
}