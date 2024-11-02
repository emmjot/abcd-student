pipeline {
    agent any
    options {
        skipDefaultCheckout(true)
    }
    stages {
        stage('Code checkout from GitHub') {
            steps {
                script {
                    cleanWs()
                    git credentialsId: 'github-token', url: 'https://github.com/emmjot/abcd-student', branch: 'main'
                }
            }
        }
        stage('Download and Install OSV-Scanner') {
            steps {
                script {
                    // Define the OSV-Scanner version
                    def osvScannerVersion = 'v1.9.1'

                    // Define OSV-Scanner download URL
                    def osvScannerUrl = "https://github.com/google/osv-scanner/releases/download/${osvScannerVersion}/osv-scanner_${osvScannerVersion}_linux_amd64"

                    // Download OSV-Scanner binary
                    sh "curl -L ${osvScannerUrl} -o osv-scanner"

                    // Make it executable
                     sh "chmod +x osv-scanner"

                    // Add current directory to PATH for the session
                    env.PATH = "${env.WORKSPACE}:${env.PATH}"
                }
            }
        }
        stage('Do something') {
            steps {
        	    sh 'pwd'
            }
        }
	}
}