pipeline{
    agent any
    stages{
        stage("Compile"){
            steps{
                sh "./gradlew compileJava"
            }
        }
        stage("Unit test"){
            steps{
                sh "./gradlew test"
            }
        }
        stage("Code coverage"){
            steps{
                sh "./gradlew jacocoTestReport"
                publishHTML(target: [
                    reportDir:'build/reports/jacoco/test/html',
                    reportFiles: 'index.html',
                    reportName: "JaCoCo Report"
                ])
                sh "./gradlew jacocoTestCoverageVerification"
            }
        }
    }
    post {
        always{
            mail to: 'montrell.story@gmail.com',
            subject: "Completed Pipeline: ${currentBuild.fullDisplayName}",
            body: "Your build completed, please check: ${env.BUILD_URL}"
        }
    }
}