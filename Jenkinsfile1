pipeline{
    agent any
    stages{
    stage('CDownload'){
        steps{
            script{
            try{
                git 'https://github.com/venkat18396/sample9.git'
            }
            catch(Exception e){
                mail bcc: '', body: 'Jenkins job failed to download git at stage "CDownload"', cc: '', from: '', replyTo: '', subject: 'JENKINS JOB CDownload', to: 'venkat.18396@gmail.com'
                abort(1)

            }
        }
        }
    }
    stage('CBuild'){
        steps{
            script{
            try{
                sh 'mvn package'
            }
            catch(Exception e){
                mail bcc: '', body: 'Jenkins job failed to at stage "CBuild"', cc: '', from: '', replyTo: '', subject: 'JENKINS JOB CBuild', to: 'venkat.18396@gmail.com'
                exit(1)
            }
            }
        }
    }
    stage('CDeploy'){
        steps{
            script{
            try{
                deploy adapters: [tomcat9(credentialsId: 'c7966982-3559-4209-b19a-2acd46dbfa78', path: '', url: 'http://172.31.62.190:8080')], contextPath: 'test', war: '**/*.war'
            }
            catch(Exception e){
                mail bcc: '', body: 'Jenkins job failed to at stage "CDeploy"', cc: '', from: '', replyTo: '', subject: 'JENKINS JOB CDeploy to QA', to: 'venkat.18396@gmail.com'
                exit(1)
            }
            }
        }
    }
    stage('CTest'){
        steps{
            script{
            try{
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/GITPL/testing.jar'
            }
            catch(Exception e){
                mail bcc: '', body: 'Jenkins job failed to at stage "CTest"', cc: '', from: '', replyTo: '', subject: 'JENKINS JOB CTest', to: 'venkat.18396@gmail.com'
                exit(1)
            }
            }
        }
    }
    stage(CDeploymenttoPROD){
        steps{
            script{
            try{
                deploy adapters: [tomcat9(credentialsId: 'c7966982-3559-4209-b19a-2acd46dbfa78', path: '', url: 'http://172.31.59.62:8080')], contextPath: 'pro', war: '**/*.war'
                mail bcc: '', body: 'Jenkins deployment to PRODUCTION HOUSE is finished with status "SUCCESS"', cc: '', from: '', replyTo: '', subject: 'JENKINS JOB Deployment', to: 'venkat.18396@gmail.com'
            }
            catch(Exception e){
                mail bcc: '', body: 'Jenkins job failed at stage "CDeploymenttoPROD"', cc: '', from: '', replyTo: '', subject: 'JENKINS JOB CTest', to: 'venkat.18396@gmail.com'
                exit(1)
            }
            }
        }
    }
    }
}
