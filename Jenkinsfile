//#!groovy
pipeline {
    agent any

    stages {
        
        
        stage('Compile') {
            steps {
             // dir('/Volumes/HD/repositorios_diplomado/ejemplo_pipeline') {  
              sh './mvnw clean compile -e'
             // }
            }
        }
        stage('Unit') {
            steps {
              // dir('/Volumes/HD/repositorios_diplomado/ejemplo_pipeline') {  
                    sh './mvnw clean test -e'
              //}
            }
        }
        stage('Jar') {
            steps {
                // dir('/Volumes/HD/repositorios_diplomado/ejemplo_pipeline') {  
                    sh './mvnw clean package -e'
              //}
            }
        }

          stage('SonarQube') {
          	steps {
    			withSonarQubeEnv('Sonar') { // You can override the credential to be used
      			sh './mvnw org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
    				}
			   }
  		}

 stage('Nexus Upload'){
                    steps {
                        nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: 'localhost:8081',
                        groupId: 'com.devopsusach2020',
                        version: '1.0.2',
                        repository: 'test-nexus',
                        credentialsId: 'credencial-nexus',
                        artifacts: [
                            [artifactId: 'DevOpsUsach2020',
                            classifier: '',
                            file: 'build/DevOpsUsach2020-1.0.2.jar',
                            type: 'jar']
                        ]
                        )
                        }
                }



        stage('Run') {
            steps {
               //dir('/Volumes/HD/repositorios_diplomado/ejemplo_pipeline') {  
                    sh 'nohup bash mvnw spring-boot:run &'
                    
              
                    
              //}
               
            }
        }
         stage('Test') {
            steps {
                sleep 20
                sh 'curl http://localhost:8081/rest/mscovid/test?msg=testing'
            }
        } 
        
       stage('Stop') {
            steps {
               //dir('/Volumes/HD/repositorios_diplomado/ejemplo_pipeline') {  
                    sh 'bash mvnw spring-boot:stop &'
                    
              
                    
              //}
               
            }
        }
       
        
 
       
    }
}