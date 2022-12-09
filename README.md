## Deploy and Expose Game 2048 on EKS Fargate using an Appplication Load Balancer

## Setup

### Step 1 - Create Cloud9 environment via AWS CloudFormation

Create CloudFormation Stack with template `/setup/cloud9.yaml`

### Step 2 - Assign instance role to Cloud9 instance

Modify IAM Role of EC2 instance for Cloud9 environment

### Step 3 - Disable Cloud9 Managed Credentials

1. Launch [AWS Cloud9 Console](https://console.aws.amazon.com/cloud9/home?region=us-east-1#)
1. Locate the Cloud9 environment created for this lab and click "Open IDE". The environment title should start with *EKSCloud9*.
1. At top menu of Cloud9 IDE, click *AWS Cloud9* and choose *Preferences*.
1. At left menu *AWS SETTINGS*, click *Credentials*.
1. Disable AWS managed temporary credentials:

  ![Disable Cloud 9 Managed Credentials](./setup/images/disable-cloud9-credentials.png)

### Step 4 - Bootstrap lab environment on Cloud9 IDE

Run commands below on Cloud9 Terminal to clone this lab repository and bootstrap the lab:

```
git clone https://github.com/phonghuule/eks-2048-game.git
cd eks-2048-game/setup
./bootstrap.sh
```

## Clean up

### Step 1

Run *cleanup.sh* from Cloud 9 Terminal to delete EKS cluster and its resources. Cleanup script will:

- Delete all the resources installed in previous steps.
- Delete the EKS cluster created via bootstrap script.

```
./cleanup.sh
```

### Step 2

Double check the EKS Cluster stack created by eksctl was deleted:

- Launch [AWS CloudFormation Console](https://console.aws.amazon.com/cloudformation/home)
- Check if the stack **eksctl-eks-alb-2048game-cluster** still exists.
- If exists, click this stack, in the stack details pane, choose *Delete*.
- Select *Delete* stack when prompted.

### Step 3

Delete the Cloud 9 CloudFormation stack named **EKS-ALB-2048-Game** from AWS Console:

- Launch [AWS CloudFormation Console](https://console.aws.amazon.com/cloudformation/home)
- Select stack **EKS-ALB-2048-Game**.
- In the stack details pane, choose *Delete*.
- Select *Delete* stack when prompted.
