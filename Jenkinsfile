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
          sh 'docker build -t gradle_app:$BUILD_NUMBER .'
          script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-cred') {
                        def image = docker.build('phalla/gradle_app:$BUILD_NUMBER')
                        image.push()
                    }
           }
         }
     }
     stage('Scan Docker Imagage'){
         steps{
            sh 'echo "docker.io/phalla/gradle_app:$BUILD_NUMBER `pwd`/dockerfile" > anchore_images'
            sh 'echo "docker.io/phalla/wordpress:1 `pwd`/dockerfile" >> anchore_images'
             anchore name: 'anchore_images'
         }
     }
   }
}
