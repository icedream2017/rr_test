node {
    stage('checkout') {
        checkout scm
    }

    stage('clean') {
        sh "./gradlew clean"
    }

    stage('assemble') {
        sh "./gradlew assemble"
    }

    stage('Test') {
        try {
            sh "./gradlew test"
        } finally {
            junit 'build/test-results/test/TEST-*.xml'
            step([$class: 'JUnitResultArchiver', testResults: 'build/test-results/test/TEST-*.xml'])
        }
    }

    stage('sonarqube') {
        sh "./gradlew -PsonarBranch=${env.BRANCH_NAME} sonarqube"
    }
}

