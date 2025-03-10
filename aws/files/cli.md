<div align="center">

# **AWS CLI (Command Line Interface)**

</div>

# Install Aws Cli

download the install file from:

    https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

    run the the file downloaded and follow the steps.

Verify  installation

    aws --version

# Configure the AWS CLI (Connect to AWS Cloud)


    shows AWS credentials
    
        cat ~/.aws/credentials
    
    Displays information about the IAM user or role making the AWS request.
    
        aws sts get-caller-identity
    
     Get Your AWS Access Key ID and Secret Access Key:

          1. Login to your AWS account and navigate to the IAM (Identity and Access Management) console.
    
          2. Click on Users and select your user.

          3. Go to the Security credentials tab, and under the Access keys section, click Create New Access Key.

          4. Download or copy the Access Key ID and Secret Access Key (you will need these to configure the AWS CLI).
      
        
    Run the AWS Configure Command:

          On Gitbash (or Powershell)

              aws configure
        
         When prompted, enter the following information:

              AWS Access Key ID: Enter the Access Key ID you got from the AWS console.
              AWS Secret Access Key: Enter the Secret Access Key you got from the AWS console.
              Default region name: Enter the AWS region you want to use (e.g., us-east-1, us-west-2, etc.). You can find the available regions here.
              Default output format: Choose the output format for the CLI (either json, text, or table).

        Test the Configuration:

             aws s3 ls

             (This will list all the S3 buckets in your AWS account. If the configuration is correct, it will show the list of S3 buckets (if any)).



        
                  
