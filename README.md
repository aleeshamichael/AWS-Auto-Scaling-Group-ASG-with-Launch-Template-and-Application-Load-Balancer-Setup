# AWS-Auto-Scaling-Group-ASG-with-Launch-Template-and-Application-Load-Balancer-Setup
## Subnet Configuration:
- **Subnet 1**: Public, 1c
- **Subnet 2**: Public, 1c
- **Subnet 3**: Private, 1c
- **Subnet 4**: Private, 1a
- **Subnet 5**: Public, 1a

## Architecture Overview:
- The private server is in **Subnet 3**, which is **not associated with the route table**.
- To access the application, we create a **Target Group (TG)** and an **Internet-facing Load Balancer (LB)**.
- **VPC**: Custom VPC.
- **Health Check Path**: Default `"var/www.html"` (double-check).
- **Application Load Balancer (ALB)**: Created for handling traffic.
- **Availability Zones (AZs)**: 1a and 1c for private instances.
- **Launch Template**: Manages instance types and configurations.

## ASG Configuration:
- **Target Tracking Policy**:
  - Metric Type: **Average CPU Utilization**
  - Target Value: **90**
- **Desired Instance Count**: **1**
- **Min & Max Scaling**: Depends on load.

## Steps to Set Up:
1. **Create a VPC.**
2. **Create 4 Subnets** (2 Public, 2 Private across at least 2 AZs).
3. **Create a Public Server.** Deploy a sample app and test it via public IP.
4. **Create an AMI** from the running public server.
5. **Create a Launch Template.** *(Optional: Test by launching an instance).*
6. **Create a Target Group (TG).**
7. **Create a Load Balancer (LB)** and associate it with the TG.
8. **Create an Auto Scaling Group (ASG)**:
   - Link to **Launch Template** → **Network** → **Target Group**.
   - Set **Target Tracking Policy** with desired min/max.

## Key Considerations:
- If ASG launches an instance in an **unsupported subnet (e.g., 1b)**, LB cannot send traffic.
- Ensure networking and target group configurations are correct.
