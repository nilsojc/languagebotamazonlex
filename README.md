<p align="center">
  <img src="diagram.png" 
</p>
  
## ☁️  Build a language translation bot using Amazon Lex ☁️

In this project, I created a language translation bot where you can input a word or a sentence into the chatbot, and it will output the translation. By combining Amazon Translate for real-time language conversion, Amazon Lex for conversational interfaces, and AWS Lambda for backend logic, such a solution can be powerful, scalable, and accessible! 🌟


<h2>Environments and Technologies Used</h2>

  - Amazon Web Services (AWS)
  - AWS Console 
  - AWS CLI
  - Amazon Lex
  - AWS Lambda
  - IAM (for managing user permissions)
  - Amazon Translate

  
<h2>Real World applications</h2>  


- 🚀 Tourism and Hospitality: Chatbots can act as virtual assistants for travelers. A chatbot in a hotel app can handle room service requests or check-in instructions in the traveler’s language.
In a tourist guide app, the chatbot can provide translated information about local attractions and services.


- 🌍 Customer Support Across Borders:
A multilingual chatbot can help businesses provide customer support in real-time across various languages, enabling them to cater to a global audience. For example: An e-commerce platform offering 24/7 support to customers in English, Spanish, French, and Chinese.
A travel agency chatbot assisting users with bookings, cancellations, and FAQs in their preferred language.


- 🏢 Corporate Training and HR Assistance:
Organizations with diverse teams can use a chatbot to assist employees in multiple languages. For corporate training, employees can ask questions in their native language, and the chatbot responds appropriately.
For HR support, the chatbot can handle queries about policies, leave requests, or payroll in various languages.






<h2>How to Build</h2>

1. **Create IAM Roles for the Tools along with creation of our empty chatbot**  
In this step, we will create the bot to start our project. We will showcase both AWS console and AWS CLI scenarios, as well as define IAM roles necessary to execute the functions.

**AWS Console option**

![image](/assets/image1.png)

**AWS CLI option**
With this option we will be utilizing AWS CLI through the cloudshell. 

First, we create an IAM role specific for Amazon Lex, Lambda and Amazon Translate usage. Make sure that the --role-name applies to the role name you want to assign:

Amazon Lex 
```
aws iam create-role \
    --role-name CaraccioloChatbotRole \
    --assume-role-policy-document '{
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Principal": {
                    "Service": "lex.amazonaws.com"
                },
                "Action": "sts:AssumeRole"
            }
        ]
    }'
```
AWS Lambda and Amazon Translate

```
aws iam create-role \
    --role-name LambdaTranslateRole \
    --assume-role-policy-document '{
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Principal": {
                    "Service": "lambda.amazonaws.com"
                },
                "Action": "sts:AssumeRole"
            }
        ]
    }'
```

Amazon Translate

Then, Attach a policy to give the necessary permissions to the roles:

Amazon Lex:
```
aws iam attach-role-policy \
    --role-name CaraccioloChatbotRole \
    --policy-arn arn:aws:iam::aws:policy/AmazonLexFullAccess
```

Amazon Translate:
```
aws iam attach-role-policy \
    --role-name LambdaTranslateRole \
    --policy-arn arn:aws:iam::aws:policy/TranslateFullAccess
```

Lambda:
```
aws iam attach-role-policy \
    --role-name LambdaTranslateRole \
    --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole
```


We can always check if the role is present along with attached policies using the following command:
```
aws iam list-attached-role-policies \
    --role-name Rolename
```
Make sure to change the 'Rolename' value to the roles that you have created and want to check. 

Then, we will create a blank bot with the existing role, leaving everything default except for option 'No' on option Children's Online Privacy Protection Act (COPPA)

```
aws lexv2-models create-bot \
 --bot-name "Caracciolo_Chatbot" \
 --description "A blank bot for conversational interfaces" \
 --role-arn "arn:aws:iam::137068224350:role/CaraccioloChatboteRole" \
 --data-privacy '{"childDirected": false}' \
 --idle-session-ttl-in-seconds 300 \
 --region "us-east-1"
```

Next, we will create the locale of the bot as 'Japanese', and build it so that it is functional:

```
aws lexv2-models create-bot-locale \
   --bot-id "<AAIICUSHKT>" \
   --bot-version "DRAFT" \
   --locale-id "ja-JP" \
   --nlu-intent-confidence-threshold 0.40 \
   --region "us-east-1"
   --role-arn "arn:aws:iam::137068224350:role/CaraccioloChatboteRole" \
```

```
aws lexv2-models build-bot-locale \
 --bot-id "<AAIICUSHKT>" \
 --locale-id "ja-JP" \
 --region "us-east-1"
```
3. **Specify Intents and Slots**  



4. **Create and test Lambda function**


5. **Final results - Testing the Chatbot**


 ---

<h2>Conclusion</h2>


