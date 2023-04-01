# AWSSERVERLESS

RECEIVE AUTOMATIC NOTIFICATIONS WITH FILE LOCATION UPON UPLOADING TO S3 BUCKET
STEP 1 :
Create an S3 Bucket with an Unique Name :

 STEP 2 :
Create an lamba function by taking  Python 3.9 as  runtime language 

STEP 3 :
Now write an Lambda function code that works for Sendind the Notifications Automatically to the User

STEP 4 :
After writing the code click on Deploy…this helps to save the code and finds the erros if any present in the code, if there any errors then it will show where the error was present.
 

CODE FOR THE LAMBDA FUNCTION :

import boto3

topic_arn = "arn:aws:sns:ap-south-1:697914187896:MYTOPIC"

def send_sns(message, subject):
    try:
        client = boto3.client("sns")
        result = client.publish(TopicArn=topic_arn, Message=message, Subject=subject)
        if result['ResponseMetadata']['HTTPStatusCode'] == 200:
            print(result)
            print("Notification sent successfully..!!!")
            return True
    except Exception as e:
        print("Error occured while publishing notification and error is : ", e)
        return False

def lambda_handler(event, context):
    print("event collected is {}".format(event))
    for record in event['Records'] :
        s3_bucket = record['s3']['bucket']['name']
        print("Bucket name is {}".format(s3_bucket))
        s3_key = record['s3']['object']['key']
        print("Bucket key name is {}".format(s3_key))
        event_name = record['eventName']
        print("Event name is {}".format(event_name))
        if "ObjectCreated" in event_name:
            from_path = "s3://{}/{}".format(s3_bucket, s3_key)
            message = "Your file is uploaded successfully to S3 bucket path: {}".format(from_path)
            subject = "Hey!! Uploaded Successfully"
        elif "ObjectRemoved" in event_name:
            message = "Your file {} has been deleted from S3 bucket {}".format(s3_key, s3_bucket)
            subject = "File Deleted from S3 bucket"
        else:
            print("Unexpected event received: {}".format(event_name))
            return False
        SNSResult = send_sns(message, subject)
        if not SNSResult:
            print("Notification failed to send..")
            return False
    print("Notifications sent for all S3 events.")
    return True



STEP 5 :
For the lambda function we have to assign the role of Administrator Access.
 
STEP 6 :
For the lambda function we need to edit the settings as memory as 1024 and storage as 1024, timeout should be as 15 min.

 STEP 7 :
For the Lambda function need to assign the S3 Triggers to trigger the lambda function while file was uploaded in S3 bucket.

STEP 8 :
To send the notifications we need to configure and topic in SNS(Simple Notification Service):

STEP 9 :
In Topic that created need to create an subscription that need to send notification via mail to the respective Mail id  

STEP 10 :
While creating an Subscription need to select the protocol as Email and the Enpoint as the respective mail id that wants to send notifications.

STEP 11 :
While adding the subscription we need to confirm the mail id that was given for subscription 

STEP 12 :
After accepting the subscription here we can find the status as confirmed.

STEP 13 :
After Creating the subscription we need to take the ARN value and that should be pasted in the Lambda function Code (EX: arn:aws:sns:ap-south-1:697914187896:MYTOPIC) , this is an ARN.

STEP 14 :
Now time to test, Upload an file to the respective S3 Bucket .

STEP 15 :
Aftet the successful Upload just open the mail that you had given in Subscription.

OUTPUT :
Files will Upload Successfully….
 
Here We go, We can see the Mail that received and here we can see the location of the file also, where the file was uploaded and the file formate too…

 
