<div align="center">

# **Lambda**
</div>

 A service that lets you run your code without managing servers. You just upload your code, and Lambda runs it in response to events (like a file upload or an API call).

Supports a variety languages.
not good for API.
not suitable for task needed to work 24/7.
good for roles like turning computers on and off.
good for moving Data from one S3 to another.

__Key Points:__

  * Serverless: You don't need to manage or provision servers.
  * Event-driven: It runs your code automatically when something triggers it (like a file being uploaded to S3 or an API request).
  * Pay-as-you-go: You only pay for the compute time your code uses (no charge for idle time).

__How to Use:__

  1. Create a Lambda Function: Write your code (in languages like Python, Node.js, etc.) and upload it to Lambda.
  2. Set a Trigger: Choose an event that will trigger your function (like an S3 file upload).
  3. Lambda Runs: When the trigger happens, Lambda automatically runs your code.
  4. Get Results: Your code executes, and Lambda sends back the result.

# Create

    Navigate to the Lambda webpage --> create function

    select the function to create (i choose Blueprint)

    Execution role - (i choose - create a new role...)

    --> create function

 __after:__

   add triger - set when the function will run.
   add destination - set wher Lambda will pass the result after doing its task
    
    
