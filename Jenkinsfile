pipeline{
   agent any
   stages{
     stage("Code Review"){
       steps{
         sh './gradlew -Dsonar.host.url=https://sonarqube.sothy.tech/ jacocoTestReport  sonarqube'
       }
     }
     stage("Buiding App"){
         steps{
          sh 'docker build -t grandle_app:$BUILD_NUMBER'
         }
     }
   }
}
