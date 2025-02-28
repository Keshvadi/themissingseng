---
title: Lambda
parent: Cloud Computing
nav_order: 94
layout: default
---

## AWS Lambda

AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers. You upload your code (or build it directly in the Lambda console), and Lambda runs it in response to _events_. You only pay for the compute time you consume – there's no charge when your code is not running. This makes Lambda a cost-effective and scalable way to run code in the cloud.

---

### Key Concepts

- **Function:** The code you upload to Lambda. Lambda supports various programming languages (Node.js, Python, Java, Go, Ruby, .NET, and custom runtimes).
- **Event:** Something that triggers your Lambda function to run. Common event sources include:
  - **API Gateway:** HTTP requests.
  - **S3:** Object uploads, deletions, or other events.
  - **DynamoDB:** Changes to a DynamoDB table.
  - **Kinesis:** Data streams.
  - **SQS:** Messages in a queue.
  - **SNS:** Notifications.
  - **CloudWatch Events/EventBridge:** Scheduled events (like cron jobs) or AWS service events.
  - **CloudFront**: triggers a Lambda function at AWS Edge locations in response to CloudFront events.
  - **Cognito**: triggers a Lambda function when ever certain Amazon Cognito events take place.
- **Trigger:** The configuration that connects an event source to a Lambda function. The trigger defines _which_ events cause the function to execute.
- **Runtime:** The environment that executes your Lambda function. Lambda provides runtimes for various languages.
- **Execution Role:** An IAM role that grants your Lambda function permissions to access other AWS services. This is how you control what your function is allowed to do (e.g., read from an S3 bucket, write to a DynamoDB table).
- **Concurrency:** The number of simultaneous executions of your Lambda function. Lambda automatically scales your function to handle incoming events, up to a configurable concurrency limit.
- **Cold Start:** The initial latency incurred when a Lambda function is invoked for the first time or after a period of inactivity. This involves setting up the execution environment. Subsequent invocations (while the environment is "warm") are much faster.
- **Layers:** A way to package libraries and other dependencies that can be shared across multiple Lambda functions. This helps keep your function deployment packages smaller and promotes code reuse.
- **Environment Variables:** Key-value pairs that you can set for your Lambda function, allowing you to configure your code without modifying it. This is useful for storing configuration settings, API keys (though using Secrets Manager is recommended for sensitive data), and other environment-specific values.
- **Dead Letter Queue**: a queue where you can redirect events that your function can't process.

---

### Example: Creating a Simple Lambda Function (Python)

This example creates a simple Lambda function that logs the event it receives and returns a "Hello" message. This can be done from AWS CLI or AWS Console. We show you using AWS Console here.

1.  **Sign in to the AWS Management Console:** Open the Lambda service.

2.  **Create a Function:**

    - Click "Create function".
    - Choose "Author from scratch".
    - **Function name:** Enter a name (e.g., `my-hello-function`).
    - **Runtime:** Select "Python 3.9" (or your desired Python version).
    - **Permissions**: Create a new role with basic permissions.
    - Click "Create function".

3.  **Write the Code:**
    In the "Code source" section, you'll see a default code editor. Replace the default code with the following:

    ```python
    import json

    def lambda_handler(event, context):
        print("Event:", json.dumps(event))
        return {
            'statusCode': 200,
            'body': json.dumps('Hello from Lambda!')
        }
    ```

    _Explanation:_

    - `lambda_handler(event, context)`: This is the _entry point_ for your Lambda function. It's the function that Lambda calls when it's invoked.
      - `event`: A dictionary containing data about the event that triggered the function. The contents of `event` depend on the event source.
      - `context`: An object containing information about the invocation, function, and execution environment.
    - `print("Event:", json.dumps(event))`: Logs the event data to CloudWatch Logs (useful for debugging).
    - `return { ... }`: Returns a response. The format of the response depends on how the function is invoked (e.g., if it's called via API Gateway, the response should be formatted as an HTTP response).

4.  **Deploy the Code:** Click the "Deploy" button to deploy your code changes.

5.  **Test the Function:**

    - Click the "Test" tab.
    - Create a new test event (you can use the default "hello-world" template). Give the test event name.
    - Click "Invoke".

    You should see the output of your function, including the logged event data and the "Hello from Lambda!" response.

---

### Configuring a Trigger (Example: S3 Trigger)

To make the function run automatically, you configure a _trigger_. This example connects the function to an S3 bucket, so the function runs whenever a new object is uploaded to the bucket.

1.  **In the Lambda function's configuration page:**

    - Click "+ Add trigger".
    - Select "S3" from the "Trigger configuration" dropdown.
    - **Bucket:** Choose the S3 bucket you want to use.
    - **Event type:** Select "PUT" (or "All object create events").
    - **Prefix/Suffix (optional):** You can optionally specify a prefix or suffix to filter the events (e.g., only trigger for files in a specific folder or with a specific extension).
    - Click "Add".

2.  **Modify Lambda Code (Optional):** You could modify your Lambda code to process the S3 event data. The `event` object will contain information about the uploaded object (bucket name, key, etc.).

    ```python
    import json

    def lambda_handler(event, context):
        bucket_name = event['Records'][0]['s3']['bucket']['name']
        object_key = event['Records'][0]['s3']['object']['key']
        print(f"File '{object_key}' uploaded to bucket '{bucket_name}'")

        return {
            'statusCode': 200,
            'body': json.dumps(f'Processed {object_key} from {bucket_name}')
        }

    ```

3.  **Update Permissions:**
    - Go to the "Configuration" tab and click on the "Permissions".
    - Click on the "Role name" link. It will open the IAM role.
    - Attach the `AmazonS3ReadOnlyAccess` policy to this role (or create a custom policy with more specific permissions).

Now, whenever you upload a file to the specified S3 bucket, your Lambda function will automatically execute.

---

### Common Use Cases

- **Serverless Web Applications:** Use API Gateway and Lambda to create RESTful APIs.
- **Real-time File Processing:** Process files as they are uploaded to S3 (e.g., image resizing, data validation).
- **Real-time Stream Processing:** Process data from Kinesis data streams.
- **Scheduled Tasks:** Run code on a schedule (e.g., daily reports, database backups).
- **Chatbots:** Build chatbots using services like Amazon Lex and Lambda.
- **IoT Backends:** Process data from IoT devices.
- **Mobile Backends:** use API gateway and lambda to implement backend for your mobile apps.

---

### Important Considerations

- **Cold Starts:** Be aware of cold start latency, especially for infrequently used functions. Provisioned Concurrency can help mitigate this.
- **Execution Time Limits:** Lambda functions have a maximum execution time (15 minutes by default). For long-running tasks, consider using AWS Batch or other services.
- **Memory Limits:** You configure the amount of memory allocated to your function. Choose an appropriate memory size based on your function's needs. The amount of memory also determines the proportional amount of CPU power.
- **Error Handling:** Implement proper error handling in your Lambda functions (e.g., using `try`/`except` blocks in Python).
- **Monitoring:** Use CloudWatch to monitor your Lambda function's invocations, errors, duration, and other metrics.
- **Cost:** Lambda pricing is based on the number of requests and the duration of your code execution. Be mindful of costs, especially for high-volume applications.
