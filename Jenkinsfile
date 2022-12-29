pipeline{
    agent any
    tools {
        maven 'Maven' 
    }

    stages{
        stage("Test"){
            steps{
                sh "mvn test"
            }
        
        }


        stage("Build"){
            steps{
                sh "mvn package"
            }
        
        }

        stage("Deploy to Test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'TestServer', path: '', url: 'http://44.201.235.52:8080/')], contextPath: '/app', war: '**/*.war'
            }
        
        }

        stage("Deploy to Prod"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'ProdServer', path: '', url: 'http://34.227.28.231:8080/')], contextPath: '/app', war: '**/*.war'
            }
        
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}