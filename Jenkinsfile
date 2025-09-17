pipeline {
agent any
tools{
maven 'my_maven'
}
stages {
stage('Build') {
steps {
echo 'This is the build'
sh 'mvn clean'
sh 'mvn compile'
}
}
stage('Test') {
steps {
echo 'This is the testing stage'
sh 'mvn test'
}
}
stage('Code Analysis') {
steps {
echo 'This is the analysis'
sh ' mvn clean verify sonar:sonar   -Dsonar.projectKey=HelloWorldTest  -Dsonar.projectName=”HelloWorldTest”   -Dsonar.host.url=http://localhost:9000   -Dsonar.token= sqp_aa307dc8b0a89e3389acf9fc6c3c1f894d920838'
}
}
stage('Deliver') {
steps {
echo 'This is the delivery stage'
sh 'cp /var/lib/jenkins/workspace/CICDPipeline/target/HelloWorld-0.0.1.jar /home/student/deploy01'
}
}
}
post {
    success {
      mail to: 'craig@creativeagilepartners.co.uk',
           subject: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
           body: "Build succeeded.\nSee: ${env.BUILD_URL}"
    }
    failure {
      mail to: 'andreas.mengel@regnology.net',
           subject: "❌ FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
           body: "Build failed.\nConsole: ${env.BUILD_URL}console"
    }
  }
}



