node
{
    def mavenHome=tool name: "maven-3.9.9"
    stage('Git Checkout')
    {
       git branch: 'development', credentialsId: 'b06ac337-17fd-4210-9a4a-c83ed569a246', url: 'https://github.com/jee1379/maven-web-app-project-kk-funda.git'
    }
    stage('COMPILE')
    {
    sh "${mavenHome}/bin/mvn clean compile"
    }
     stage('Build')
     {
        sh "${mavenHome}/bin/mvn clean package"
     }
     stage('SQ REPORT')
     {
     sh "${mavenHome}/bin/mvn clean sonar:sonar"
     }
     stage('Deploy to nexus')
     {
    sh  "${mavenHome}/bin/mvn clean deploy"
	}
	stage('Deploy to Tomcat') {
        echo "Deploying WAR file using curl..."

        sh """
            curl -u jeevan:jeevan1 \
            --upload-file /var/lib/jenkins/workspace/
jio-Scripted-dev-PL/target/maven-web-application.war \
            "http://54.242.158.30:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """
    }

    
} //node ending 
