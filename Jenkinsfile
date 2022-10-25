node {
    checkout scm
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