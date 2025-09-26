pipeline{
    agent {label 'docker'}

    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/mohamedbstar413/calculator.git'
            }
        }
    }
    
}