pipeline {
    agent any

    stages {
         stage('cleanWs') {
            steps {
                echo 'clean workspace'
                //clean workspace before init
                cleanWs()
            }
        }
        stage('gitinit') {
            steps {
                echo 'gitinit'
                git branch: 'main', url: 'https://github.com/Elad0109/simple-webapp-nodejs-.git'
            }
        }
        stage('build') {
            steps {
                echo 'build'
                nodejs('nodejs') {
                    //run build
                    sh 'npm  install'
                }
            }
        }
        stage('test') {
            steps {
                echo 'test'
                nodejs('nodejs') {
                    //run test
                    sh 'npm  run test'
                }
               
            }
        }
        stage('display') {
            steps {
                echo 'display'
                nodejs('nodejs') {
                    //run display
                    sh 'npm run start'
                }
               
            }
        }
        
    }
}
