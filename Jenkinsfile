node('master') {
    stage('Cont Download branch'){
        git 'https://github.com/venkatbanda9/MyJavaApp.git'
    }
    stage('Cont Build branch'){
        sh 'mvn package'
    }
}
