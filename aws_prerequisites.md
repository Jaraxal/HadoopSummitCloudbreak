# Launching Cloudbreak on AWS
Before launching Cloudbreak on AWS, review and meet the prerequisites.

## Meet the Prerequisites
Before launching Cloudbreak on AWS, you must meet the following prerequisites.

 - [AWS Account](#aws-account)
 - [AWS Region](#aws-region)
 - [SSH Key Pair](#ssh-key-pair)
 - [Key Based Authentication](#Key-Based-Authentication)
  
 ### AWS Account
 In order to launch Cloudbreak on AWS, you must log in to your AWS account. If you don't have an account, you can create one at https://aws.amazon.com/.
 ### AWS Region
 Decide in which AWS region you would like to launch Cloudbreak. The following AWS regions are supported:
![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/Regions.png)
 ### SSH Key Pair
 Import an existing Key Pair or generate a new Key Pair in the AWS region which you are planning to use for launching Cloudbreak and clusters. **You need this SSH Key Pair to SSH to the Cloudbreak instance and Start Cloudbreak.** To do this use the following steps.

  - Navigate to the Amazon EC2 console at https://console.aws.amazon.com/ec2/.
 
  - Check the region listed in the top right corner to make sure that you are in the correct region.
 
  - In the left pane, find NETWORK AND SECURITY and click Key Pairs.
 
  - Do one of the following:
 
    To generate a new Key Pair:
   
      - Click Create Key Pair to create a new key pair
    
      - Your private Key file will be automatically downloaded onto your computer.
    
      - Make sure to save it in a secure location. You will need it to SSH to the cluster nodes. 
    
      - You may want to change access settings for the file using chmod 400 my-key-pair.pem.

   
    To import an existing Public Key:
   
     - Click Import Key Pair to upload an existing Public Key 
    
     - Select the Public Key and click Import.
   
     - Make sure that you have access to its corresponding Private Key.


 ### Key Based Authentication
  
If you are using key-based authentication for Cloudbreak on AWS, you must be able to provide your AWS Access Key and Secret Key pair. Cloudbreak will use these keys to launch the resources. You must provide the Access and Secret Keys later in the Cloudbreak web UI later when creating a credential.

If you choose this option, all you need to do at this point is check your AWS account and make sure that you can access this Key Pair. You can generate new access and secret keys from the IAM Console.

To do this go to the IAM Service:
 1. In the left pane click on Users > Select a user 
 
 2. Click on the Security credentials tab
 
 3. Creat Access Key or use an existing Access Key. There is a limit of two.

![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/AWS_Users.png)
![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/CreateAccessKey.png)
  
To create a new user go to IAM Service:

 1.In the left pane click on Users > Select Add User
 
 2.Enter a user name, select Programming access and then click on Next: Permissions
![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/aws_add_user_1.png)

 3.For Set Permissions keep the defaul "Add usert to group"
 
 4.In Add User to group select all the groups then click Next:Review 
 
 5.Review your choices and click on Create User
 
![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/aws_add_user_2.png)

6.If your user has been created successfully you will see a similar image as below

![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/aws_add_user_3.png)


7.Once you are done with these steps [you can proceed to Launch the VM.](README.md)  
