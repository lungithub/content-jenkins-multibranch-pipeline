pipeline {
  agent any

  stages {
    stage('build') {
      steps {
        sh 'javac -d . src/*.java'
        sh 'echo Main-Class: Rectangulator > MANIFEST.MF'
        sh 'jar -cvmf MANIFEST.MF rectangle.jar *.class'
      }

  post {
    success {
      archiveArtifacts artifacts: 'rectangle.jar', fingerprint: true
     }
    }
   }
    stage('run') {
      steps {
        sh 'java -jar rectangle.jar 7 9'
      }
    }


stage('Promote Development to Master') {
  when {
    branch 'devbranch1'
  }
  steps {
    echo 'Stashing Local Changes'
    sh 'git stash'
    echo 'Checking Out Development'
    sh 'git checkout devbranch1'
    sh 'git pull origin'
    echo 'Checking Out Master'
    sh 'git checkout master'
    echo 'Merging Development into Master'
    sh 'git merge devbranch1'
    echo 'Git Push to Origin'
    sh 'git push origin master'
  }
  }
}
