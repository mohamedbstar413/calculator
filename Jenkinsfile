pipeline {
    agent { label 'docker' }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        gradle 'gradle'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/mohamedbstar413/calculator.git'
            }
        }
        stage('Compile') {
            steps {
                dir('calculator-app') {
                    sh 'gradle compileJava'
                }
            }
        }
        stage('Unit Test') {
            steps {
                dir('calculator-app') {
                    sh 'gradle test'
                }
            }
        }

        stage('Code Coverage') {
            steps {
                dir('calculator-app') {
                    sh 'gradle jacocoTestReport'
                    publishHTML(target: [
                        reportDir: 'build/reports/jacoco/test/html',
                        reportFiles: 'index.html',
                        reportName: 'JaCoCo Report'
                    ])
                    sh 'gradle jacocoTestCoverageVerification'
                }
            }
        }
        stage('Gradle Build') {
            steps {
                dir('calculator-app') {
                    sh 'gradle build'
                }
            }
        }
        stage('Docker Build') {
            steps {
                withCredentials([usernamePassword(credentialsId:'dockerhub', usernameVariable:'username', passwordVariable: 'password')]) {
                        sh "echo $password| docker login -u $username --password-stdin"
                        dir('calculator-app') {
                            sh 'docker build -t calculator .'
                        }
                }
            }
        }
        stage('Push To Docker hub') {
            steps {
                dir('calculator-app') {
                    //tag image
                    sh 'docker tag calculator mabdelsattar413/calculator'
                    //push image
                    sh 'docker push mabdelsattar413/calculator'
                }
            }
        }
    }
}
