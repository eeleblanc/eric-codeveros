node {
    stage('cleanup'){
        cleanWs()
    }
    checkout scm
    dir('services/ui/angular') {
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
    }
}