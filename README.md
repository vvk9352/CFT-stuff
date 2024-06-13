# CloudFormation Template for EC2 Instances with VPC Setup

## Overview

This CloudFormation template is designed to test various resources in AWS CloudFormation. It includes the creation of a VPC, Subnets, Route Tables, Security Groups, and EC2 instances with both Linux and Windows configurations. The instances are configured with user-provided usernames and passwords, and have HTTP and SSH/RDP access as appropriate.

## Template Structure

### Mappings

Mappings for AMI IDs are defined for various AWS regions, both for Linux and Windows instances. These mappings allow the template to select the appropriate AMI based on the specified region and OS type.

### Parameters

- `username`: A string parameter for the username to be created on the instances.
- `password`: A string parameter for the password for the created user.
- `AMIType`: A string parameter to specify the type of AMI to use (Linux, Windows, or Both).
- `InstanceType`: A string parameter to specify the EC2 instance type. Defaults to `t2.micro`.
- `KeyName`: An AWS EC2 Key Pair Name for SSH access to the instances.

### Conditions

- `Ec2Launchlinux`: Condition to launch Linux EC2 instances based on the AMIType.
- `Ec2LaunchWindows`: Condition to launch Windows EC2 instances based on the AMIType.
- `WindowsSec`: Condition to apply security settings for Windows instances.
- `LinuxSec`: Condition to apply security settings for Linux instances.

### Resources

1. **VPC and Networking**
    - `CreateVPC`: Creates a VPC with a CIDR block of 10.0.0.0/16.
    - `CreateSubnetone`: Creates a subnet within the VPC.
    - `CreateRoutetable`: Creates a route table for the VPC.
    - `Createinternetgateway`: Creates an Internet Gateway for the VPC.
    - `VPCgateway`: Attaches the Internet Gateway to the VPC.
    - `Routetableinternetgateway`: Adds a route to the route table to allow internet access.
    - `SubnetoneRoutetable`: Associates the subnet with the route table.

2. **Security Groups**
    - `SecurityGroupsLinux`: Security group for Linux instances allowing SSH, HTTP, and ICMP access.
    - `SecurityGroupsWindows`: Security group for Windows instances allowing RDP, HTTP, and ICMP access.

3. **EC2 Instances**
    - `EC2instancelaunchLinux`: Launches a Linux EC2 instance with user data to set up a user, password, and a basic HTTP server.
    - `EC2instancelaunchWindows`: Launches a Windows EC2 instance with user data to set up a user, password, and a basic IIS web server.

## Usage

1. **Parameters to Fill:**
   - `username`: Enter the username for the instance.
   - `password`: Enter the password for the created user.
   - `AMIType`: Choose the type of AMI (`Linux`, `Windows`, or `Both`).
   - `InstanceType`: Select the EC2 instance type (e.g., `t2.micro`).
   - `KeyName`: Enter the Key Pair Name for SSH/RDP access.

2. **Deployment Steps:**
   - Upload the template to AWS CloudFormation.
   - Fill in the parameters as per your requirements.
   - Deploy the stack and wait for the resources to be created.

## Notes

- The template ensures that either or both Linux and Windows instances are launched based on the `AMIType` parameter.
- Security groups are configured to allow necessary access (SSH for Linux, RDP for Windows, HTTP, and ICMP for both).
- UserData scripts for both Linux and Windows instances set up a basic web server and create a user with the provided credentials.

This template is an excellent way to understand and experiment with AWS CloudFormation features, creating a robust environment with networking, security, and compute resources.
##Promote open-source learning!
