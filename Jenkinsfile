pipeline {
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        timeout(time: 120, unit: 'MINUTES')
    }
    agent {
        label 'OpenJDK8'
    }
    tools {
        maven "Maven 3.3"
        jdk "OpenJDK 1.8"
    }
    // Environment variables
    //environment {
    //}
    stages {
        stage ('Run Package') {
            steps {
                script {
                    sh "mvn clean package -Dmaven.test.skip=true"
                    //sh "mvn clean deploy -Dmaven.test.skip=true"
                    //sh "mvn jetty:run"
                    }
                }
            }
        stage ('Run Tests') {
            steps {
                echo "Running sonar test"
                script {
                    sh "mvn clean test"
                    sh "mvn clean integration-test"
                    sh " mvn clean verify"
                }
            }
        }
        //stage ('Run Sonar') {
        //    steps {
        //        echo "Running sonar test"
        //        script {
        //            SONAR_OPTS = "-Dmaven.test.failure.ignore=true --fail-never -Dsonar.branch.name=${branchName} " +
        //                    "-Dsonar.language=java -Dsonar.exclusions=**/gen/**,**/src/main/java/gov/niem/**," +
        //                    "**/src/main/java/gov/hhs/cms/ffe/irsreporting/domain/irs/**," +
        //                    "-Dsonar.projectKey=gov.hhs.cms.ffe.batch:EE-batch-apps-parent," +
        //                    "**/webapp/js/*.js,**/*.min.js,**/webapp/test/**/*.js,**/webapp/js/lang/*.js"
        //
        //            sh "mvn -P default,sonar7 sonar:sonar ${SONAR_OPTS}"
        //        }
        }
}
