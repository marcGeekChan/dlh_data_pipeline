pipeline {
    agent {
        dockerContainer  {
            image 'r-base:4.5.3'
        }
    }

    stages {
        stage('Run Script') {
            steps {
                sh '''
                # Run the script
                Rscript pileline.R
                '''
            }
        }
    }
}