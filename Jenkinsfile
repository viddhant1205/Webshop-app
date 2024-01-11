pipeline {
    agent any
    
    tools{
        jdk 'jdk17' 
    }
    
    
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }
    
    stages {
        stage('Github Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/viddhant1205/Python-Webapp.git'
            }
        }
      
         stage('CLJ-HOMES-SCAN') {
            steps {
                sh "clj-holmes fetch-rules"
                sh "clj-holmes scan -p ./"
            }
        }

        stage('Sonarqube') {
            steps {
                withSonarQubeEnv('sonar-server'){
                   sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=WebShop-App \
                      -Dsonar.projectKey=WebShop-App '''
               }
            }
        }
        
        stage('Docker Build & Deploy') {
            steps {
                   sh "docker-compose up -d "
               }
           } 
        
        }
 }
