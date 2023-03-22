node
{
    def mavenHome = tool name: "maven3.9.1"
    stage ('CheckoutCode')
    {
        git branch: 'development', credentialsId: '72fd4c72-939e-42a8-85ce-dcdff1a4c11f', url: 'https://github.com/romeDevOpsTraining/maven-web-application.git'
    }
    stage ('Build')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage ('ExecuteSQReport')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage ('UploadArtifactIntoNexus')
    {
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage ('UploadArtifactIntoTomcat')
    {
        sshagent(['1b77c96c-f071-45dc-914a-837fe41207b5']) 
        {
            sh 'scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.239.230.130:/opt/tomcat/webapps/'
        }
    }
}
