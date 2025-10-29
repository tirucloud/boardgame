pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3.6'
    }

    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout from Git') {
            steps {
                git branch: 'main', url: 'https://github.com/tirucloud/boardgame.git'
            }
        }
        stage("Maven build")
        {
         steps {
                sh 'mvn clean package'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh '''
                        $SCANNER_HOME/bin/sonar-scanner \
                        -Dsonar.projectName=Boardgame \
                        -Dsonar.projectKey=Boardgame
                    '''
                }
            }
        }

        stage('Quality Gate') {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }

        stage('Trivy FS Scan') {
            steps {
                sh 'trivy fs . > trivyfs.txt'
            }
        }

        stage('Docker Build & Tag') {
            steps {
                script {
                    sh 'docker build -t boardgame .'
                    sh 'docker tag boardgame tirucloud/boardgame:latest'
                }
            }
        }

        stage('Trivy Image Scan') {
            steps {
                sh 'trivy image tirucloud/boardgame:latest > trivyimage.txt'
            }
        }

        stage('Docker Push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh 'docker push tirucloud/boardgame:latest'
                    }
                }
            }
        }

        stage('Deploy to Container') {
            steps {
                sh '''
                docker rm -f boardgame || true
                docker run -d --name boardgame -p 8081:8080 tirucloud/boardgame:latest
                '''
            }
        }
         stage('Deploy to EKS') {
            steps {
                withCredentials([[
                $class: 'AmazonWebServicesCredentialsBinding',
                credentialsId: 'aws-cred'
                ]]) {
                sh '''
                aws eks update-kubeconfig --region us-east-1 --name tiru-cluster
                kubectl apply -f Kubernetes/ds.yml --validate=false
                '''
                }
            }
         }
    }
    post {
        always {
            emailext(
                attachLog: true,
                subject: "${currentBuild.result}",
                body: """
                    <b>Project:</b> ${env.JOB_NAME}<br/>
                    <b>Build Number:</b> ${env.BUILD_NUMBER}<br/>
                    <b>URL:</b> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a><br/>
                """,
                to: 'tirucloud@gmail.com',
                attachmentsPattern: 'trivyfs.txt,trivyimage.txt'
            )
        }
    }
}
