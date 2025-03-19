pipeline{
    agent any
   stages{
        stage('Build'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
           steps{
            echo 'hello world'
            sh 'npm --version'
            sh 'node --version'
            sh '''
            npm ci
            npm run build
            ls -la 
            '''
            }
         }
         stage('Test'){
            steps{
               echo 'Test Stage'
            }
           
         }
    }
}