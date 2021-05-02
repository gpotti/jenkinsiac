pipeline {
  agent any
  parameters{
    booleanParam(name: 'Static_Check',
      defaultValue: false,
      description: 'Checkbox Parameter')
    booleanParam(name: 'QA',
      defaultValue: false,
        description: 'Checkbox Parameter')
    booleanParam(name: 'Unit_Test',
      defaultValue: false,
        description: 'Checkbox Parameter')
    String(name: 'Success_Email',
      defaultValue: 'govicloudarch@gmail.com',
        description: 'mail id for success usecase')    
    String(name: 'Failure_Email',
      defaultValue: 'govicloudarch@gmail.com',
        description: 'mail id for failure usecase')  
  }
  stages {
    stage('Git Pull') {
      steps {
        echo 'Pull repo from Git'
        git 'https://github.com/gpotti/jenkinsiac.git'
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
