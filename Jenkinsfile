node
{
    def mavenHome = tool name:"maven-3.6.3"
    stage('code checkout')
    {
        git credentialsId: '94437543-dc2c-4453-ab06-bb9ea15660f0', url: 'https://github.com/pavanireddy-1/maven-web-application'
    }
    stage('build')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('sonarqube report')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('artifact')
    {
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage('DeployAppIntoTomcat')
    {
        sshagent(['3fe680c5-59f6-4b49-8b1d-61e2224c4bff']) {
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@15.206.84.68:/opt/apache-tomcat-9.0.29/webapps/"
}

    }
    stage('EmailNotification')
    {
        emailext body: '''Build is Over !!

regards,
Pavani G''', subject: 'build is over !!!!', to: 'pavanireddy667@gmail.com'
    }
}
