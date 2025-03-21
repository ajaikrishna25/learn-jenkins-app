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
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
               
               sh '''
               echo 'Test Stage'
               test -f build/index.html
               npm test
               '''
            }
           
         }
         stage('E2E'){
            agent{
                docker{
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
            steps{
               
               sh '''
               npm install -serve
               snode_modules/.bin/serve -s build
               npx playwright test
               '''
            }
           
         }
    }
    post{
        always{
            echo "post section"
            junit 'test-results/junit.xml'
        }
    }
}