pipeline {
        agent none
        stages {
		  stage("Checkout") {
            agent any
            steps {
                sh 'https://github.com/gvsiva2008/mvn-sonar.git'
            }
          }
          stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('My SonarQube Server') {
                sh 'mvn clean package sonar:sonar'
              }
            }
          }
          stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
        }
      }
