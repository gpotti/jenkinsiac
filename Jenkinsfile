pipeline {
  agent any
  stages {
    stage('Git Pull') {
      steps {
        echo 'Pull repo from Git'
      }
    }

    stage('Checking holiday') {
      steps {
        echo 'Step to call rest api and check if its a holiday'
      }
    }

    stage('Build') {
      steps {
        echo 'Build if it is not a holiday as returned from previous'
      }
    }

    stage('Static Check') {
      steps {
        echo 'Execute if not a holiday and static_check parameter is selected'
      }
    }

    stage('QA') {
      steps {
        echo 'If not holiday, if QA checkbox enabled and if static check passes'
      }
    }

    stage('Summary') {
      steps {
        echo 'List all the executed steps'
      }
    }

  }
}