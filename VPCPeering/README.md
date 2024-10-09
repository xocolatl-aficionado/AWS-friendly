## VPC A, B and C peered and wired.....through CloudFormation

### VPC Peers arent transitive. 

To peer VPC A, B and C, therefore, we need 3 peering relationships 
- ```A - B```, 
- ```A - C``` and 
- ```B - C```. 

Of course, adding the peering relationship is not enough. We also need to add routing. 

To illustrate this setup, 
1. we use a single subnet created in each of the VPCs A, B and C, 
2. add routing to each routing table in each VPC to point to the corresponding VPC peering connection within the respective VPC```pcx-```,
3. deploy private EC2 instances to each VPC's private subnet, 
4. create security groups for each of these EC2 instances, 
5. and associate the appropriate rules in the security group to allow traffic to and from the other 2 VPCs

**Acceptance Criteria**: Starting with VPCA, VPCB and VPCC with CIDRs 10.16.0.0/16, 10.17.0.0/16 and 10.18.0.0/16 respectively, we should be able to enter the EC2 instance in VPCA and ```ping``` the instance in VPCB and VPCC using their _private_ IPs.

**Results**

<img width="1021" alt="Screenshot 2024-10-09 at 6 10 12 AM" src="https://github.com/user-attachments/assets/2a1992e5-6fb6-4873-a153-c2670a81da26">

 **Final CloudFormation Setup**

<img width="1318" alt="Screenshot 2024-10-09 at 6 13 12 AM" src="https://github.com/user-attachments/assets/83db78bd-874e-4c2c-a0f9-00c25258c899">
<img width="655" alt="Screenshot 2024-10-09 at 6 12 16 AM" src="https://github.com/user-attachments/assets/42d9bbda-847e-4352-99e0-db34072d8974">
