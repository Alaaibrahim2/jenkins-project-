node {
    deleteDir() 

    stage('Checkout') {
        git branch: 'main', url: 'https://github.com/Alaaibrahim2/jenkins-pro.git'
    }

    stage('Build') {
        try {
            sh 'echo "build stage"'
        } catch (Exception e) {
            sh 'echo "found exception"'
            throw e
        }
    }

    stage('Test') {
        if (env.BRANCH_NAME == 'feat') {
            sh 'echo "test stage"'
        } else {
            sh 'echo "skip test stage"'
        }
    }
}
