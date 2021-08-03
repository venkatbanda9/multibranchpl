node('master') {
    stage('Cont Download master'){
        git 'https://github.com/venkatbanda9/MyJavaApp.git'
    }
    stage('Cont Build master'){
        sh 'mvn package'
    }
    stage('Cont Deploy for testing master'){
        deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://50.18.246.232:8080')], contextPath: 'testingapp', war: '**/*.war'
    }
}
node('slave'){
    stage('Cont Test master'){
        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
        sh 'java -jar /home/ec2-user/workspace/workspace/ScriptedPipeline/testing.jar'
    }
}
node('master'){
    stage('Build Transfer from Master to slave_MASTER'){
        sh 'scp /var/lib/jenkins/workspace/ScriptedPLDeployFromSlave/webapp/target/webapp.war ec2-user@3.236.165.43:/home/ec2-user/workspace/workspace/ScriptedPLDeployFromSlave/test.war'
    }
}
node('slave'){
    stage('Cont Delivery_MASTER'){
        sh 'scp /home/ec2-user/workspace/workspace/ScriptedPLDeployFromSlave/test.war ec2-user@54.183.225.22:/var/www/html/production.war'
    }
}
