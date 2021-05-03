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
        println today.format("yyyy-MM-dd")
        def holidays = httpRequest 'https://calendarific.com/api/v2/holidays?&api_key=48de66774abaace74f8e418c644ae0ad9517fed2&country=IN&year=d'
        println("Status: "+holidays.status)
        writeJSON(file: 'holidays.json', json: holidays)
        }
      }
    }

  stages {
    stage('Build') {
      steps {
        echo 'Build if it is not a holiday as returned from previous'
      }
    }
  parallel {
   stages {
    stage('Static Check') {
      steps {
        script {
          if (params.Static_Check) {
            echo 'Static Check - Yes'
            stchkpass = true
          } else {
            echo 'Static Check - No'
            stchkpass = false 
          }
        }          
      }
    }

    stage('QA') {
      steps {
        script {
          if (stchkpass) {
              if (params.QA) {
                  echo 'QA - Yes'
                } else {
                  echo 'QA - No'
                }
           }
         }
      }
     }
    }
  stages {
    stage('Unit Test') {
      steps {
        script {
              if (params.Unit_Test) {
                  echo 'Unit Test - Yes'
                } else {
                  echo 'Unit Test - No'
                }
         }
      }
     }
    }
    }
  }
    
    
    stage('Summary') {
      steps {
        echo 'List all the executed steps'
      }
    }

  }
}
