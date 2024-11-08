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
        stage('Run TruffleHog') {
            steps {
                script {
                    sh 'trufflehog git --branch main https://github.com/emmjot/abcd-student --json > trufflehog.json'
                    // Run the OSV-Scanner command
                    //sh '/mnt/c/toolsABC/osv-scanner_windows_amd64.exe --lockfile=/mnt/c/gitABC/abcd-student/package-lock.json > osv-scan-results.txt'
                    //sh 'osv-scanner scan --lockfile package-lock.json --json > sca-osv-scanner.json'
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
    post {
        always {
	        //echo 'Archiving results...'
		    //archiveArtifacts artifacts: 'results/**/*', fingerprint: true, allowEmptyArchive: true
		    echo 'Sending reports to DefectDojo...'
		    defectDojoPublisher(artifact: 'trufflehog.json', productName: 'Juice Shop', scanType: 'Trufflehog Scan', engagementName: 'jasek.marcin@gmail.com')
		    //defectDojoPublisher(artifact: 'results/sca-osv-scanner.json', productName: 'Juice Shop', scanType: 'OSV Scan', engagementName: 'jasek.marcin@gmail.com')
		}
	}

}