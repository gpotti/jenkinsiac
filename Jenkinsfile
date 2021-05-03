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
    text(name: 'Success_Email',
      defaultValue: 'govicloudarch@gmail.com',
        description: 'mail id for success usecase')    
    text(name: 'Failure_Email',
      defaultValue: 'govicloudarch@gmail.com',
        description: 'mail id for failure usecase')  
  }
  stages {
    stage('Git Pull') {
      steps {
        echo 'Pull repo from Git'
      }
    }

    stage('Checking holiday') {
      steps {
        script {
        echo 'Step to call rest api and check if its a holiday'
        isHoliday = false
        def today = new Date()
        println today
        def response = httpRequest 'https://calendarific.com/api/v2/holidays?&api_key=48de66774abaace74f8e418c644ae0ad9517fed2&country=IN&year=2021'
        println("Status: "+response.status)
        writeJSON(file: 'holidays.json', json: response)
        }
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
