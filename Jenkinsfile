pipeline{
    agent {label 'docker'}

    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/mohamedbstar413/calculator.git'
            }
        }
        stage('Compile'){
            steps{
                sh './calculator-app/gradlew compileJava'
            }
        }
        
    }
    
}