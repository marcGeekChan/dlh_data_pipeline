pipeline {
    agent {
        docker  {
            image 'r-base:4.5.3'
        }
    }

    environment {
        GITHUB_PAT = credentials('github')
    }

    stages {
        stage('Install remotes') {
            steps {
                sh '''
                Rscript -e "install.packages('remotes', repos='https://cloud.r-project.org')"
                '''
            }
        }
        stage('Run Script') {
            steps {
                withCredentials([file(credentialsId: 'renviron', variable: 'RENVI_FILE')]) {
                    sh '''
                    cp $RENVI_FILE ~/.Renviron
                    Rscript -e "Sys.setenv(GITHUB_PAT ='${GITHUB_PAT }'); remotes::install_github('marcGeekChan/pipelineR')"
                    '''
                }
            }
        }
    }
}