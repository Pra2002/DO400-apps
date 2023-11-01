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
                        dir("${env.WORKSPACE}/shopping-cart-v2/"){
                            sh './mvnw test -D testGroups=unit'
                        }
                    }
                }
                stage("Build"){
                    dir("${env.WORKSPACE}/shopping-cart-v2/"){
                        sh './mvnw package -D skipTests '
                    }
                }
                stage('Integreation tests'){
                    when {
                        expression{params.RUN_INTEGRATION_TESTS==true}
                    }
                    steps{
                        dir("${env.WORKSPACE}/shopping-cart-v2/"){
                       sh './mvnw test -D testGroups=integration'
                        }
                    }
                }
            }
            }

        }
}