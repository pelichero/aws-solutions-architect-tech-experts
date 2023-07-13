





=======================================================================

1 - What should you use to control traffic in and out of EC2 instances?
Network Access Control List (NACL)
[x]Security Groups
IAM Polices

Security Groups operate at the EC2 instance level and can control traffic



2 - Security Groups can be attached to only one EC2 instance.
True
[x]False

Security Groups can be attached to multiple EC2 instances within the same AWS Region/VPC.



3 - What does this CIDR 10.0.4.0/28 correspond to?
[x]10.0.4.0 to 10.0.4.15
10.0.4.0 to 10.0.32.0
10.0.4.0 to 10.0.4.28
10.0.0.0 to 10.0.16.0

/28 means 16 IPs (=2^(32-28) = 2^4), means only the last digit can change.


You plan on creating a subnet and want it to have at least capacity for 28 EC2 instances. What's the minimum size you need to have for your subnet?

/28
/27
[x] /26
/25


Security Groups operate at the ................. level while NACLs operate at the ................. leve
[x] EC2 instance, Subnet
Subnet, EC2 instance


You have attached an Internet Gateway to your VPC, but your EC2 instances still don't have access to the internet. What is NOT a possible issue?

Route table are missing entries
The EC2 instance don't have public IP
[x] The security group does not allow traffic in
The NACL does not allow network traffic out

Security groups are stateful and if traffic can go out, then it can go back in.


VPC Peering has been enabled between VPC A and VPC B, and the route tables have been updated for VPC A. But, the EC2 instances cannot communicate. What is the likely issue?

Check NACL
[x] Check Route table in VPC B
Check EC2 instance attached Security Group
Check if DNS resolution is enabled

Route tables must be updated in both VPCs that are peered.


Networking: 
https://start.jcolemorrison.com/aws-vpc-core-concepts-analogy-guide/