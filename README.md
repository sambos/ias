# Infra as Code
Infrastructure as code worked examples


### AWS Session Manager 
Connect to Windows using RDP through Session Manager without opening ports in security groups

https://reinvent2019.aws-management.tools/mgt406/en/optional/step7.html

**Pre-req:**
Install aws cli
Install RDP Client
Install AWS Session Manager Plugin
RDP Port Forward

Steps:
* Start session-manager/ssm session on windows ec2 from console, this will start the power shell command prompt
* Create user (you can also assign the user to administrator group or another if needed)
``` powershell
# create a password for the user
$password = Read-Host -AssecureString  
# create user with your password
New-LocalUser "SampleUser" -Password $password
#add user to a group
Add-LocalGroupMember -Group "Remote Desktop Users" -Member "SampleUser"
```
* Command to port forward,  be sure to get your aws windows ec2 instance-id as
``` powershell
aws ssm start-session --target <instance-id> --document-name AWS-StartPortForwardingSession --parameters "localPortNumber=55678,portNumber=3389"

# start RDP and point to localhost:55678 and provide user
enter passwrod when prompted 

enjoy!
```
