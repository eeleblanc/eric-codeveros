node {
    stage('Cleanup'){
        cleanWs()
    }
    checkout scm
    dir('services/ui/angular') {
        /*
        stage('Dependencies') {
            docker.image('node:14.16').inside {
                sh 'npm ci --quiet --cache="./npm"'
            }
        }
        stage('Build') {
            docker.image('node:14.16').inside {
                sh 'npm run build.production --cache="./npm"'
            }
        }
        stage('Lint') {
            try {
                echo 'Linting'
            } catch(Exception e) {
                echo 'Failed Linting ' + e.toString()
            }
        }
        stage('Test') {
            docker.image('buildkite/puppeteer:8.0.0').inside {
                sh 'npm run test --cache="./npm"'
            }
        }
        */
        stage('Deliver') {
            if(env.BRANCH_NAME=='master') {
                docker.withRegistry('','dockerhub') {
                    def myImage = docker.build("eeleblanc/ui:${env.BUILD_ID}")
                    myImage.push()
                    myImage.push('latest')
                }
            }
        }
    }
}