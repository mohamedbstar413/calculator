pipeline{
    agent {label 'docker'}
    triggers{
        pollSCM('* * * * *')
    }
    tools{
        gradle 'gradle'
    }

    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/mohamedbstar413/calculator.git'
            }
        }
        stage('Compile'){
            steps{
                dir('calculator-app'){
                    sh 'gradle compileJava'
                }
            }
        }
        stage('Unit Test'){
            steps{
                dir('calculator-app'){
                    sh 'gradle test'
                }
            }
        }

        stage('Code Coverage'){
            steps{
                dir('calculator-app'){
                    sh 'gradle jacocoTestReport'
                    publishHTML (target: [
                        reportDir: 'build/reports/jacoco/test/html',
                        reportFiles: 'index.html',
                        reportName: "JaCoCo Report"
                    ])
                    sh 'gradle jacocoTestCoverageVerification'
                }
            }
        }
    }
    
}