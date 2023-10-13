STEP 1 > Create a S3 bucket

STEP 2 > edit the Bucket Policy use "S3-policy-dev-fooder_acc.json" file
         edit the file as required ( "Principal": { "Service": "logs.<REGION>.amazonaws.com" }, )
                                   ( "Resource": "arn:aws:s3:::<BUCKET_NAME>", )
                                   ( "aws:SourceAccount": ["<ACCOUND_ID_WITHOUT_indentation>"] )
                                   ( "aws:SourceArn"["<ARN_of_the_CLOUD_WATCH_LOG-GROUP>"] )

STEP 3 > Creae IAM Role for Lambda (ETL ROLE)
         IAM -> Roles -> Create -> edit Permisions -> add (s3-full-access)
                                                          (cloudwatch-access)
                                                          (lambda-execution)
                                -> edit trust-relationship -> ( "Service": [ "lambda.amazonaws.com",
                                                                             "logs.amazonaws.com",
                                                                             "delivery.logs.amazonaws.com" ])

STEP 4 > Create AWS Lambda function ( Author from scratch, use python & add the above created Role)

STEP 5 > COPY code from "export_cloudwatchlogs_to_s3.py" ->
         edit the file as required ( e.g. NDAYS = 1 )

STEP 6 > Deploy

Step 7 > Add a trigger for the above created Lambda function
         Create a EVENET-BREDGE -> crate new rule -> rule-type = Schedule expression -> e.g. rate(1 day)
