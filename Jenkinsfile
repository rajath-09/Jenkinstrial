pipeline {
  agent any
  stages {
    stage ('Build') {
      steps {
        sh 'printenv'
        sh 'docker build -t rajath-09/jenkinstrial:""$GIT_COMMIT"" .'
      }
    }
 
    stage ('Publish to ECR') {
      steps {
        //sh 'aws ecr-public get-login-password --region eu-west-2 | docker login --username AWS --password-stdin public.ecr.aws/t7e2c6o4'
        //withAWS(credentials: 'sam-jenkins-demo-credentials', region: 'eu-west-2') {
         withEnv(["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"]) {
          sh ' docker login -u AWS -p $(aws ecr get-login-password --region ap-south-1) 570110885728.dkr.ecr.ap-south-1.amazonaws.com'
          sh 'docker build -t jenkinstrial .'
          sh 'docker tag jenkinstrial:latest 570110885728.dkr.ecr.ap-south-1.amazonaws.com/jenkinstrial:""$BUILD_ID""'
          sh 'docker push 570110885728.dkr.ecr.ap-south-1.amazonaws.com/jenkinstrial:""$BUILD_ID""'
         }
       }
    }
  }
}
