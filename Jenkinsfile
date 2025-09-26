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
                sh 'gradle compileJava'
            }
        }
        stage('Unit Test'){
            steps{
                sh './calculator-app/gradlew test'
            }
        }
    }
    
}