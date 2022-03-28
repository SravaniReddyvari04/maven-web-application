node
{
    def MavenHome = tool name: "Maven_3.8.2"
    
    stage('Checkout code'){
        git branch: 'development', credentialsId: '05d28452-2421-4ff5-a4cd-787ae2cc461f', 
        url: 'https://github.com/SravaniReddyvari04/maven-web-application.git'
    }
    
    stage('Build'){
        sh "${MavenHome}/bin/mvn clean package"
    }
    
    stage('Execute Sonarqube report'){
        sh "${MavenHome}/bin/mvn clean sonar:sonar"
    }
    
    stage('Deploy artifacts'){
        sh "${MavenHome}/bin/mvn clean deploy"
    }
    
    stage('deploying app into Tomcat'){
    sshagent(['3b058f02-118a-410e-80b1-fc5876e39b00']) {
    sh "scp -o StrictHostKeychecking=no target/maven-web-application.war ec2-user@15.206.80.97:/opt/apache-tomcat-9.0.60/webapps"
}
}
}
