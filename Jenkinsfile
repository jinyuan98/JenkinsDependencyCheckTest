pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                git '/home/JenkinsDependencyCheckTest'
            }
        }

        stage('OWASP DependencyCheck') {
            steps {
                dependencyCheck additionalArguments: ''' 
                            -o './'
                            -s './'
                            -f 'ALL' 
                            --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
							'--format HTML --format XML --suppression suppression.xml'
                
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
    }    
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
