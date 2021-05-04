pipeline {
    agent any

    stages {
        stage('prepratiom') {
            steps {
                git "https://github.com/Maymaher/jenkins_nodejs_example"
            }
        }
         stage('CI') {
            steps {
                   withCredentials([usernamePassword(credentialsId: 'jenkins', passwordVariable: 'mypass', usernameVariable: 'myname')])
                   {
                    sh """
                    docker build . -t mai/myimage:1.0
                    docker login --username ${myname} --password ${mypass}
                    docker push mai/myimage:1.0
                    
                    """
                   }
            }
        }
        
        stage('CD') {
            steps {
                   withCredentials([usernamePassword(credentialsId: 'jenkins', passwordVariable: 'mypass', usernameVariable: 'myname')])
                   {
                   
                   sh """
                    docker run -d -p 3000:3000 mai/myimage:1.0
                    """
                   }
                   
            }
        }
    }
}
