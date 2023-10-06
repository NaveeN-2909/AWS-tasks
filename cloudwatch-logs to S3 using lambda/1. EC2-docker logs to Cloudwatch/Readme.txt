STEP 1 > crate a IAM policy using the "docker-cloudwatch-logging-driver-ec2-role-policy.json" file
          edit the file as equired ( YOURAWSACCOUNT => account ID )
                                   ( log-group:NAME-OF-THE-LOG_GROUP:* ) # to narror the permision 
                                   ( log-group:*:* ) # applies to all the log-groups

STEP 2 > Create a IAM Role for cloudwatch & attatch the above craeted policy + add "ssm policy" to this Role

STEP 3 > Create EC2 or edit the EC2 instance to use the above craeted Role

STEP 4 > Create a Log-Group in the CloudWatch Console

STEP 5 > RUN the docker Container with required args 
        --log-driver="awslogs" # default for cloudwatch
        --log-opt awslogs-region=us-east-1  # change based on your EC2
        --log-opt awslogs-group="myapp/dev" # Log-Group name tha was created in STEP 4
        --log-opt awslogs-stream="myapp-log-stream" # name of the log-stream of your choice

STEP 6 > Verify from the cloudwatch console -> log-roups -> log stream 

STEP 7 > these logs can be manually exported to S3 at a certain point-in-time.
         to automate this lets use lambda in the next steps