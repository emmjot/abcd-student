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
        //stage('Download and Install OSV-Scanner') {
        //    steps {
        //        script {
        //            // Define the OSV-Scanner version
        //            def osvScannerVersion = 'v1.9.1'

                    // Define OSV-Scanner download URL
        //            def osvScannerUrl = "https://github.com/google/osv-scanner/releases/${osvScannerVersion}/osv-scanner_windows_amd64"

                    // Download OSV-Scanner binary
        //            sh "curl -L ${osvScannerUrl} -o osv-scanner"

                    // Make it executable
        //             sh "chmod +x osv-scanner"

                    // Add current directory to PATH for the session
        //            env.PATH = "${env.WORKSPACE}:${env.PATH}"
        //        }
        //    }
        //}
                        // https://github.com/google/osv-scanner/releases/tag/v1.9.1/osv-scanner_windows_amd64.exe
        stage('Install OSV-Scanner') {
            steps {
                // Pobranie i zainstalowanie OSV-Scanner, jeśli nie jest zainstalowany globalnie
                sh '''
                if ! [ -x "$(command -v osv-scanner)" ]; then
                    curl -LO https://github.com/google/osv-scanner/releases/download/v1.0.0/osv-scanner-linux-amd64
                    chmod +x osv-scanner-linux-amd64
                    sudo mv osv-scanner-linux-amd64 /usr/local/bin/osv-scanner
                fi
                '''
            }
        }
        stage('Run OSV-Scanner for package-lock.json') {
            steps {
                script {
                    // Run the OSV-Scanner command
                    sh './osv-scanner --lockfile=package-lock.json > osv-scan-results.txt'
                    //sh './osv-scanner --lockfile=package-lock.json > osv-scan-results.txt'
                    //sh '''
                    //    osv-scanner scan --lockfile package-lock.json
                    //    sleep 15
                    //   '''
                    // Optionally print the results
                    //sh 'cat osv-scan-results.txt'
                }
            }
        }
	}
}