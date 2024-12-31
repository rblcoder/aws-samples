## Debug unable to delete VPC endpoint

Asked the following question:
'''
I am unable to delete an App runner requested VPC endpoint even though the apprunner service is deleted. I have also deleted Network configurations under AWS App Runner. What further steps need to be followed?
'''

Amazon Q answer
'''
I understand you're having trouble deleting a VPC endpoint that was requested by App Runner, even though you've deleted the App Runner service and its network configurations. Let's investigate this issue and determine the next steps to resolve it.

First, let's gather some information about the VPC endpoint:

Described VPC Endpoints

Using the ec2.describe_vpc_endpoints tool in us-east-1

It seems that there are no VPC endpoints currently associated with App Runner requests. This is unexpected given your description of the problem. Let's double-check by looking for all VPC endpoints:

Described VPC Endpoints

Using the ec2.describe_vpc_endpoints tool in us-east-1

It appears there is a VPC endpoint, but it's not directly associated with App Runner. Let's analyze the information we have:

VPC Endpoint ID: vpc endpoint id
State: available
Service Name: com.amazonaws.vpce....
VPC ID: vpc id
Requester Managed: true
Tags:
AMQManaged: true
Broker: broker id
This VPC endpoint appears to be managed by Amazon MQ (based on the AMQManaged tag), not App Runner. This explains why deleting the App Runner service and network configurations didn't remove this endpoint.

Here are the steps you should follow to address this situation:

Verify Amazon MQ usage:

Check if you're still using Amazon MQ in your AWS account, particularly the broker with ID b-2f4bf092-429d-41ef-b4e9-7efbea4f1e5d.
If you're no longer using this broker, you should delete it first.
Delete the Amazon MQ broker


Go to the Amazon MQ console.
Find the broker with ID broker id.
Delete this broker if it's no longer needed.
Wait for VPC endpoint deletion:

After deleting the Amazon MQ broker, wait for a few minutes. AWS should automatically delete the associated VPC endpoint.

'''
