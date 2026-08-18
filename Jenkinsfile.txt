Pipeline
{
  Agent any
  stages{
       stage('Clone-Repo')
    {
      steps{
        checkout scm
      }
    }
         stage('Build')
    {
      steps{
        sh 'mvn install'
      }
    }
         stage('Compile')
    {
      steps{
        sh 'mvn clean compile'
      }
    }
         stage('Run Test')
    {
      steps{
        sh 'mvn test'
      }
    }
         stage('Packege as WAR')
    {
      steps{
        sh 'mvn package'
      }
    }
         stage('Deployment')
    {
      steps{
        sh 'scp target/sample-java-app-1.0.0.jar root@172.31.45.60:/root/tomcat/apache-tomcat-10.1.57/webapps'
      }
    }
  }
}
