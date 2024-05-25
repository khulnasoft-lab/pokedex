// make sure to add "kengine-api-key" to your Jenkins credentials prior to running this pipeline

pipeline {
    agent any

    stages {

        stage("Push and Report") {

            agent {
                docker {
                    image 'khulnasoft/kengine:0.0.30'
                    args '--entrypoint='
                    reuseNode true
                }
            }

            environment {
                KENGINE_API_KEY = credentials('kengine-api-key')
            }

            input {
                message "Do you want to push the changes?"
                ok "Yes"
            }

            steps {
                // this step will push the changes without asking for confirmation again
                sh 'kengine push -y --c .kengine'
                sh 'kengine report --c .kengine'
            }
        }
    }
}
