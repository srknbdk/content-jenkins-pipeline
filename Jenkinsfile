pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'javac -d . src/*.java'
        sh 'echo Main-Class: Rectangulator > MANIFEST.MF'
        sh 'jar -cvmf MANIFEST.MF rectangle.jar *.class'
      }
    }
    stage('run') {
      parallel {
        stage('run') {
          environment {
            type = 'x'
          }
          steps {
            sh 'java -jar rectangle.jar 7 9'
          }
        }
        stage('parallel') {
          environment {
            type = 'xxx'
          }
          steps {
            readFile(file: 'README.md', encoding: 'UTF8')
          }
        }
      }
    }
    stage('deneme') {
      steps {
        echo 'Oldu sanki..'
      }
    }
  }
  post {
    success {
      archiveArtifacts(artifacts: 'rectangle.jar', fingerprint: true)

    }

  }
}