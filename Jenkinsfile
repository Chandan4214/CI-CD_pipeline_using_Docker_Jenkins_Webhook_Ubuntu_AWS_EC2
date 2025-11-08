pipeline{
    agent any
    environment {
      CONTAINER_NAME = "nestjs_app"
      IMAGE_NAME = "nestjs_image"
      EMAIL="cs762585@gmail.com"
      PORT=3000
    }

    stages{
        stage('clone repo'){
          steps{
            git branch: "main", url:'https://github.com/Chandan4214/CI-CD_pipeline_using_Docker_Jenkins_Webhook_Ubuntu_AWS_EC2'
          }

        }

        stage('build docker image'){
          steps{
            sh "docker build -t $IMAGE_NAME ."
          }
        }
        stage('stop and remove '){
          steps{
            sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
            '''
          }
        }
        stage('build container and run'){
          steps{
            sh '''
                docker run -d -p $PORT:$PORT --name $CONTAINER_NAME $IMAGE_NAME
            '''
          }
        }
        
        stage('send email notification'){
          steps{
            emailext(
              subject: "Deployment Successful: NestJS Application is Live",
              body: "Your NestJS application is live at http://13.200.19.42:$PORT",
              to: "$EMAIL"
            )
          }
        }  


    }


}
