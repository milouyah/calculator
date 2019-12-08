pipeline {
    agent any
    triggers {
          pollSCM('* * * * *')
     }
    stages {
        stage("Checkout") {
            steps {
                git url: 'https://github.com/milouyah/calculator.git'
            }
        }
        stage("Compile") {
            steps {
                sh "./gradlew compileJava"
            }
        }
        stage("Unit test") {
            steps {
                sh "./gradlew test"
            }
        }
          stage("Code coverage") {
               steps {
                    sh "./gradlew jacocoTestReport"
                    sh "./gradlew jacocoTestCoverageVerification"
               }
          }
          stage("Package") {
               steps {
                    sh "./gradlew build"
               }
          }

          stage("Docker build") {
               steps {
                    sh "docker build -t milouyah/calculator ."
               }
          }

    }
}