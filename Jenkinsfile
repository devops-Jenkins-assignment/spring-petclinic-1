pipeline{
  agent{label 'node-jdk-17'}
  triggers {
    pollSCM('* * * * *')
  }
  parameters {
    choice(name:'MAVEN_GOAL',choices:['package','install','clean'],description:'Maven Goal')
  }
     stages{
        stage('vcm')
        {
            steps {
                git url :'https://github.com/devops-Jenkins-assignment/spring-petclinic-1.git',
                branch : 'develop'
            }
        }
        stage('package for develop environment'){  
            tools {
                jdk 'JDK-17'
            }    
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
            }
        }
        stage('post build for develop environment') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }

   }

}