# AWSSERVERLESS
![image](https://user-images.githubusercontent.com/90970301/229303771-380bc97d-a890-4af6-a9e1-395faf77f0a1.png)


RECEIVE AUTOMATIC NOTIFICATIONS WITH FILE LOCATION UPON UPLOADING TO S3 BUCKET
STEP 1 :
Create an S3 Bucket with an Unique Name :
![image](https://user-images.githubusercontent.com/90970301/229303799-9619e56c-5a4d-4a2d-b281-36a6bc593d53.png)


 STEP 2 :
Create an lamba function by taking  Python 3.9 as  runtime language 
![image](https://user-images.githubusercontent.com/90970301/229303812-75bbbb24-45c1-4acf-a6f6-a98540003359.png)

STEP 3 :
Now write an Lambda function code that works for Sendind the Notifications Automatically to the User
![image](https://user-images.githubusercontent.com/90970301/229303821-d23f5f49-2209-42d2-acb1-f756c393a318.png)


STEP 4 :
After writing the code click on Deploy…this helps to save the code and finds the erros if any present in the code, if there any errors then it will show where the error was present.
 

STEP 5 :
For the lambda function we have to assign the role of Administrator Access.
![image](https://user-images.githubusercontent.com/90970301/229303870-51cb2c1a-3935-41b0-99a6-79199f132da2.png)

 
STEP 6 :
For the lambda function we need to edit the settings as memory as 1024 and storage as 1024, timeout should be as 15 min.
![image](https://user-images.githubusercontent.com/90970301/229303878-2bad440f-ce1c-4861-94cc-c3fc63b66ea2.png)


 STEP 7 :
For the Lambda function need to assign the S3 Triggers to trigger the lambda function while file was uploaded in S3 bucket.
![image](https://user-images.githubusercontent.com/90970301/229303889-cbebacd7-56f5-432c-83e1-f176a599cfdf.png)


STEP 8 :
To send the notifications we need to configure and topic in SNS(Simple Notification Service):
![image](https://user-images.githubusercontent.com/90970301/229303896-4390e448-074d-48cc-9657-9dbda48a7538.png)

STEP 9 :
In Topic that created need to create an subscription that need to send notification via mail to the respective Mail id  
![image](https://user-images.githubusercontent.com/90970301/229303903-e13588e6-1a5e-4e0e-932e-c65ee8b84ca4.png)


STEP 10 :
While creating an Subscription need to select the protocol as Email and the Enpoint as the respective mail id that wants to send notifications.
![image](https://user-images.githubusercontent.com/90970301/229303906-5d084957-8bc7-43c0-983a-7389a6e25e5d.png)
![image](https://user-images.githubusercontent.com/90970301/229303919-60168cb4-dcdc-47f3-8326-890fc6ef92c6.png)



STEP 11 :
While adding the subscription we need to confirm the mail id that was given for subscription 
![image](https://user-images.githubusercontent.com/90970301/229303925-ff5909fb-9d4e-4d9a-92d5-d0ba1ce0f25e.png)

![image](https://user-images.githubusercontent.com/90970301/229303931-d4c6cca8-3cd3-4e1c-8517-9ae3c619b273.png)

STEP 12 :
After accepting the subscription here we can find the status as confirmed.
![image](https://user-images.githubusercontent.com/90970301/229303939-aa4b4c24-2b84-4bfd-8dac-455f683668ab.png)


STEP 13 :
After Creating the subscription we need to take the ARN value and that should be pasted in the Lambda function Code (EX: arn:aws:sns:ap-south-1:697914187896:MYTOPIC) , this is an ARN.
![image](https://user-images.githubusercontent.com/90970301/229303945-bd89b8b8-977e-4b47-b4ae-626182588223.png)

STEP 14 :
Now time to test, Upload an file to the respective S3 Bucket .
![image](https://user-images.githubusercontent.com/90970301/229303951-21cd0998-e632-470b-b6ff-9312a4236cd0.png)

STEP 15 :
Aftet the successful Upload just open the mail that you had given in Subscription.
![image](https://user-images.githubusercontent.com/90970301/229303961-8c029acf-1783-4b14-8637-629c9187d8ab.png)

OUTPUT :
Files will Upload Successfully….
![image](https://user-images.githubusercontent.com/90970301/229303970-64c14c6b-3996-4226-8154-7bd738d5ad86.png)

 
Here We go, We can see the Mail that received and here we can see the location of the file also, where the file was uploaded and the file formate too…
![image](https://user-images.githubusercontent.com/90970301/229303977-d39bfa01-2e11-4682-a837-41e0d17037c5.png)

 
