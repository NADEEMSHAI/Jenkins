pipeline {
    agent { label 'jdk-8' }
    triggers {
        pollSCM( '* * * * *' )
    }
    parameters {
        choice(name: 'jdk-8', choices: [ 'mvn install', 'mvn package', 'mvn clean' ], description: 'pick one' )
    }
    tools {
        jdk 'jdk-8'
    }
    stages {
        stage('vcs'){
            steps { 
                git url: 'https://github.com/NADEEMSHAI/game-of-life.git'
                }
        }
        stage('packages'){
            steps {
                sh 'java -version'
                sh 'mvn package'
            }
        }  
    }
}