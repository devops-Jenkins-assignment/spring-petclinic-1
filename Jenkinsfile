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
                branch : 'staging'
            }
        }
        stage('package for staging environment'){  
            tools {
                jdk 'JDK-17'
            }    
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
            }
        }
        stage('post build for staging environment') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }

   }

}