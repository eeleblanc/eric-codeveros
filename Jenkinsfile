def servicePath = 'services/ui/angular'
def imageRepo = 'eeleblanc/ui'
node {
    stage('Cleanup'){
        cleanWs()
    }
    checkout scm
    dir(servicePath) {
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
            if(env.BRANCH_NAME=='develop') {
                docker.withRegistry('','dockerhub') {
                    def myImage = docker.build("${imageRepo}:${env.BUILD_ID}")
                    myImage.push()
                    myImage.push('dev')
                }
            }
        }
        stage('Promote') {
            if(env.BRANCH_NAME=='master') {
                docker.withRegistry('','dockerhub') {
                    def myImage = docker.image("${imageRepo}:dev")
                    myImage.pull()
                    myImage.push('latest')
                }
            }
        }
    }
}