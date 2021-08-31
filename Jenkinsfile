pipeline{
    agent {
        label 'docker-amt'
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '30'))
        timestamps()
        timeout(unit: 'HOURS', time: 2)
    }
    stages{
        stage('Cloning Repository') {
            steps{ 
                script{
                    scmCheckout {
                        clean = true
                    }
                }
            }
        }
        stage('Static Code Scan') {
            steps{
                script{
                    staticCodeScan {
                        // generic
                        scanners             = ['checkmarx', 'protex', 'snyk']
                        scannerType          = 'javascript'

                        protexProjectName    = 'OpenAMT - UI Toolkit-react'
                        // internal, do not change
                        protexBuildName      = 'rrs-generic-protex-build'

                        checkmarxProjectName = "OpenAMT - UI Toolkit-react"

                        //snyk details
                        snykManifestFile        = ['package-lock.json']
                        snykProjectName         = ['openamt-ui-toolkit-react']
                    }
                }
            }
        }
    }
}