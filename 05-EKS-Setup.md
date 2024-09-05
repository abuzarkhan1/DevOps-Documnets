## Step - 1 : Create EKS in AWS #

1) Launch a new Ubuntu VM using AWS EC2 (t2.micro).
2) Connect to the machine and install `kubectl` using the following commands:

    ```bash
    curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
    chmod +x ./kubectl
    sudo mv ./kubectl /usr/local/bin
    kubectl version --short --client
    ```

3) Install the latest version of AWS CLI using the following commands:

    ```bash
    sudo apt install unzip
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    unzip awscliv2.zip
    sudo ./aws/install
    aws --version
    ```

4) Install `eksctl` using the following commands:

    ```bash
    curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
    sudo mv /tmp/eksctl /usr/local/bin
    eksctl version
    ```

## Step - 2 : Create IAM Role & Attach to EKS Management Host #

1) Create a new IAM Role using the IAM service (Select Usecase - EC2).
2) Add the following permissions to the role:
    - IAM - FullAccess
    - VPC - FullAccess
    - EC2 - FullAccess
    - CloudFormation - FullAccess
    - Administrator - Access

3) Enter Role Name (`eksroleec2`).
4) Attach the created role to the EKS Management Host (Select EC2 => Click on Security => Modify IAM Role => Attach the IAM role we created).

## Step - 3 : Create EKS Cluster Using `eksctl` #

**Syntax:**

```bash
eksctl create cluster --name cluster-name  \
--region region-name \
--node-type instance-type \
--nodes-min 2 \
--nodes-max 2 \ 
--zones <AZ-1>,<AZ-2>

## N. Virgina: <br/>
`
eksctl create cluster --name abuzar-cluster4 --region us-east-1 --node-type t2.medium  --zones us-east-1a,us-east-1b
`	
## Note: Cluster creation will take 5 to 10 mins of time (we have to wait). After cluster created we can check nodes using below command.

`
 kubectl get nodes  
`

## Note: We should be able to see EKS cluster nodes here.**

# We are done with our Setup 


