pipeline{
    agent any 
    parameters{
        booleanParam (name : "RUN_INTEGRATION_TESTS",defaultValue: true)
    }
    stages{
        stage("Test"){
            parallel{
                stage('Unit test'){
                    steps{
                         sh './mvnw test -D testGroups=unit'
                    }
                }
                stage('Integreation tests'){
                    when {
                        expression{param.RUN_INTEGRATION_TESTS==true}
                    }
                    steps{
                       sh './mvnw test -D testGroups=integration'
                    }
                }
            }
            }

        }
}