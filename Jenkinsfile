#!groovy
node {

   stage('Stage 1'){
      echo 'Hello there, shell scripts'
   }

   stage('Checkout'){
      git url: 'https://github.com/lzhengqc/jenkins-pipeline-shell-scripts.git'
   }

   stage('Permission Setting'){
      sh 'chmod +x *.sh'
   }

   stage('Build'){
      sh './myBuild.sh'    
   }

   stage('Test'){
        parallel 'functional': {
          sh './myTest.sh' 
          sleep 30
        }, 'performance': {
           sh './myTest.sh'  // Test can seperated to different tests  ex: Integration and Qualit , Functional , Load and security
           sleep 20
        } 
     }


   stage('Aproval'){
      timeout(time:20, unit:'SECONDS') {  // DAYS , MINUTES
           input 'Do you approve deployment?'
      }
   }

   stage('Deploy'){     
      sh './myDeployment.sh'
   }
}
