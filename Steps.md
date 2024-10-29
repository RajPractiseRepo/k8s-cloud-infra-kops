# KOPS BINARY INSTALLATION
# KUBECTL BINARY INSTALLATION

# Launch an Ubuntu VM on AWS

# SETUP IAM Role
In order to build cluster within AWS, we’ll create a dedicated IAM Role for KOPS. Create the Role and attach it to the EC2 client machine.
The KOPS user will require the following IAM permissions to function properly.
1.	AmazonEC2FullAccess
2.	AmazonRoute53FullAccess
3.	AmazonS3FullAccess
4.	AmazonVPCFullAccess

# Set Up an S3 Bucket for kops Configuration.
kops uses an S3 bucket to store cluster configuration.

# Set Up Route 53 and DNS Configuration
To manage DNS for Kubernetes, I set up Route 53 and linked it to my domain purchased via Hostinger.

# Configure Hostinger DNS:
•	updated the Hostinger DNS records by pasting the Route 53 nameservers to ensure traffic was redirected correctly.

# CREATE SSH KEY FOR NODE AUTHENTIFICATION
ssh-keygen

• SSH Key will be generated in .ssh/ folder

# CREATING KOPS CLUSTER:
• We’re ready now to start creating our cluster! Let’s first set up a few environment variables to make this process easier.

# Setting up env variables:

export NAME=cloudopswithswapnil.in \
export KOPS_STATE_STORE=s3://cloudopswithswapnil.in \
export AWS_REGION=us-east-1 \
export CLUSTER_NAME=cloudopswithswapnil.in \
export EDITOR='/usr/bin/nano' \

# Create a Cluster using Kops and generate a cluster file.

kops create cluster --name=cloudopswithswapnil.in \
--state=s3://cloudopswithswapnil.in --zones=us-east-1a,us-east-1b \
--node-count=2 --control-plane-count=1 --node-size=t3.medium --control-plane-size=t3.medium \
--control-plane-zones=us-east-1a --control-plane-volume-size 10 --node-volume-size 10 \
--ssh-public-key ~/.ssh/id_ed25519.pub \
--dns-zone=cloudopswithswapnil.in --dry-run --output yaml

# Once done run below commands to create the cluster 

kops create -f cluster.yml
kops update cluster --name cloudopswithswapnil.in --yes --admin
kops validate cluster --wait 10m
kops delete -f cluster.yml  --yes

# Note: FOR MULTI AVAILABILITY ZONE CLUSTER
kops create cluster — zones us-east-1a, us-east-1b $ {NAME}

# LIST THE CLUSTER
![k8s-cluster](https://github.com/user-attachments/assets/a6f1cec2-6419-405e-aefe-d813d9da7471)

# CONCLUSION

By following this Steps, you should now have a fully functioning Kubernetes cluster running on AWS using KOPS. 






