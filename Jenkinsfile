#!groovy
properties([disableConcurrentBuilds()])

pipeline {
    agent {
            label 'prod'  //deploy on dev server
         }
    triggers {pollSCM('* * * * *')}
       options {
               buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10')) 
               timestamps()
               timeout(time: 1, unit: 'HOURS')
//               ansiColor('xterm')
       }
    stages {
              stage("checkout") {
                       steps {
                               echo "=========== Begin Update NPM version ==========="
                               sh 'sudo npm install -g npm@latest'
                               echo "=========== End Update NPM version ==========="
                       }
               }  
               stage("install-deps") {
                      steps {
                               echo "=========== Begin Install dependencies ==========="
                               sh 'npm ci'
                               echo "=========== End Install dependencies ==========="
                       }
               } 

               stage("build-packages") {
                      steps {
                               echo "=========== Begin Build ==========="
                               sh 'npm run build'
                               echo "=========== End Build ==========="
                       }
               }         
               stage("run-unit-tests") {
                      steps {
                               echo "=========== Begin Test ==========="
                               sh 'npm run test'
                               echo "=========== End Test ==========="
                       }
               }        
      } 
 }
