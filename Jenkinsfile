pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
    
    agent none
    stages{
            stage('compile'){
                agent any
                steps{
                    sh 'mvn compile'
                }
            }
            stage('codereview'){
                agent any
                steps{
                    sh 'mvn pmd:pmd'
                }
                post{
                    always{
                        pmd pattern: 'target/pmd.xml'
                    }
                }
            }
            stage('unittest'){

                steps{
                    git 'https://github.com/ashudevopss/DevOpsClassCodes.git'
                    bat 'mvn test'
                }
                post{
                    always{
                        junit 'target/surefire-reports/*.xml'
                    }
                }
                
            }
            stage('metriccheck'){
                agent any
                steps{
                    sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
                }
                post{
                    always{
                        cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                    }
                }
            }
            stage('package'){
                agent any
                steps{
                    sh 'mvn package'
                }
            }
    }
}
