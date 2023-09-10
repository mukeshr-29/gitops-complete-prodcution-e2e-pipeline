pipeline {
    agent any
    
    environment {
        APP_NAME = "complete-production-pipeline"
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }
    
    
        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url:'https://github.com/mukeshr-29/
                gitops-complete-prodcution-e2e-pipeline.git'
            }
        }
    

    
        stage("Update the Deployment Tags") {
            steps {
                sh """
                    cat deployment.yaml
                    sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                    cat deployment.yaml
                """
            }
        }

        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                    git config --global user.name "mukeshr-29"
                    git config --global user.email "mukesh@gmail.com"
                    git add deployment.yaml
                    git commit -m "mine"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                    sh "git push https://github.com/mukeshr-29/gitops-complete-prodcution-e2e-pipeline main"
                }
            }
        }

    }

}
