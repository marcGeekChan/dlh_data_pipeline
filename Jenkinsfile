pipeline {
    agent {
        docker {
            image 'r-base:4.5.3'
        }
    }

    environment {
        GITHUB_PAT = credentials('github')  // Jenkins secret with your PAT
    }

    stages {
        stage('Install and Run Script') {
            steps {
                withCredentials([file(credentialsId: 'renviron', variable: 'RENVI_FILE')]) {
                    sh '''
                    # Optional: copy .Renviron if you need other environment variables
                    cp $RENVI_FILE ~/.Renviron || true

                    # Install remotes and the GitHub package in the same Rscript session
                    Rscript -e "
                    install.packages('remotes', repos='https://cloud.r-project.org');
                    Sys.setenv(GITHUB_PAT='${GITHUB_PAT}');
                    remotes::install_github('marcGeekChan/pipelineR')
                    "
                    '''
                }
            }
        }
    }
}