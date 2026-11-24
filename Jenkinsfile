pipeline {
    agent none

    stages {

        // Stage 1: Build
        stage('build') {
            agent {
                label 'build'
            }

            steps {
                // Clean the workspace
                deleteDir()

                // Clone the GitHub repository
                sh '''
                    git clone https://github.com/Sachin75751/Portfolio-Website.git
                    ls -la
                '''

                // Save files for the Deploy stage
                stash name: 'Webpage', includes: 'Portfolio-Website/**'
            }
        }

        // Stage 2: Deploy
        stage('deploy') {
            agent {
                label 'deploy'
            }

            steps {
                // Clean the workspace
                deleteDir()

                // Retrieve files from Build stage
                unstash 'Webpage'

                // Copy website files to the web server
                sh '''
                    sudo rm -rf /var/www/html/*
                    sudo cp -r Portfolio-Website/* /var/www/html/
                    ls -la /var/www/html
                '''
            }
        }
    }
}
