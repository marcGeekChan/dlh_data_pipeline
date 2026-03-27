pipeline {
    agent {
        docker  {
            image 'r-base:4.5.3'
        }
    }

    environment {
        GITHUB_TOKEN = credentials('github')
    }

    stages {
        stage('Run Script') {
            steps {
                withCredentials([file(credentialsId: 'renviron', variable: 'RENVI_FILE')]) {
                    sh '''
                    cp $RENVI_FILE ~/.Renviron
                    Rscript -e "Sys.setenv(GITHUB_TOKEN='${GITHUB_TOKEN}'); remotes::install_github('marcGeekChan/pipelineR')"
                    '''
                }
            }
        }
    }
}