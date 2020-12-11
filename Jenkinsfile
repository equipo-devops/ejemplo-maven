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
                        nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'test-nexus',
                         packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '',
                          extension: 'jar', filePath: 'build/DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020',
                           groupId: 'com.devopsusach2020', packaging: 'jar', version: '1.0.2']]]
                        }
                }



      /*  stage('Run') {
            steps {
               //dir('/Volumes/HD/repositorios_diplomado/ejemplo_pipeline') {  
                    sh 'nohup bash mvnw spring-boot:run &'
                    
              
                    
              //}
               
            }
        }*/
       /*  stage('Test') {
            steps {
                sleep 20
                sh 'curl http://localhost:8081/rest/mscovid/test?msg=testing'
            }
        } */
        
       /*stage('Stop') {
            steps {
               //dir('/Volumes/HD/repositorios_diplomado/ejemplo_pipeline') {  
                    sh 'bash mvnw spring-boot:stop &'
                    
              
                    
              //}
               
            }
        }*/
       
        
 
       
    }
}