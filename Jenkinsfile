@Library('Shared') _
pipeline{
    agent { label  'worker'}
    environment{
        IMAGE_NAME = 'doc105b/notes_app'
        TAG = '3.0'
    }
    
    stages{
        stage('Code'){
            steps{
                script{
                    clone('main','https://github.com/namanSingh101/django-notes-app/')
                }
            }
        }
        stage('Build'){
            steps{
               script{
                   build(IMAGE_NAME,TAG)
               }
            }
        }
        stage('Login'){
            steps{
                script{
                    dockerCred('dockerhub-creds')
                }
            }
        }
        stage('Image Push'){
            steps{
                script{
                    pushImage(IMAGE_NAME,TAG)
                }
            }
        }
        stage('Test'){
            steps{
                echo 'Testing the code'
                script{
                    buildpipe()
                }
            }
        }
        stage('Deploy'){
            steps{
                echo 'Deploying the code'
            }
        }
    }
}
