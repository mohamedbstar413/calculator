pipeline{
    agent {label 'docker'}
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
    }
    
}