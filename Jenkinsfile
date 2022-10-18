pipeline { 
    environment { 
        registry = "kowsalya1809/kss" 
        registryCredential = 'kowsalya-dockerhub' 
        dockerImage = '' 
    }
    agent any 
 // triggers{
 //       cron('45 9 * * *')
 //   }
    stages { 
      stage('Build') {
         steps {
            sh 'java -version'
            sh 'chmod +x gradlew'
           sh "./gradlew assemble -PbuildNumber=${env.BUILD_ID} -PbranchName=${env.BRANCH_NAME}"
       }
    }
        
    stage('Test'){
      steps{
        withGradle {
          sh './gradlew test'
        }
      }  
    }
        
        stage('Building our image') { 
            steps {
                  script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                }
            } 
        }
