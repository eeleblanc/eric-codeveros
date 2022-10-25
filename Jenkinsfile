node {
    checkout scm
    dir('services/ui/angular') {
        stage('Dependencies') {
            docker.image('node:14.16').inside {
                sh 'npm ci --quiet --cache="./npm"'
            }
        }
        stage('Build') {
            echo 'Hello World'
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