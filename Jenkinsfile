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
          sh 'docker build -t grandle_app:$BUILD_NUMBER .'
         }
     }
     stage('Scan Docker Imagage'){
         steps{
            sh 'echo "grandle_app:5 `pwd`/Dockerfile" > anchore_images'
             anchore name: 'anchore_images'
         }
     }
   }
}
