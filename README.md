# Setup-Kubernetes-Cluster-with-KOPS-using-AWS

# Introduction

This document explains how i successfully created a kubernetes cluster using KOPS.

# Prerequisites:
AWS EC2
AWS Route 53
AWS IAM
AWS S3 Bucket
KOPS 
KUBECTL
Go Daddy 

Step 1: Create an EC2 Ubuntu Instance, set up key pairs, set up security group.

Step 2: Create AWS S3 Bucket to store your clusters state, download credentials after.

Step 3: Set up IAM User and give it administrator priviledges.

Step 4: Create a route53 domain for your cluster.

Step 5: Link the Amazon Hosted Zone to Godaddy DNS. This handles traffic routing

Step 6: Log on to the AWS EC2 instance, run an update commabnd and install aws cli
Command: sudo apt update && sudo apt install awscli -y

Step 7: Set up AWS s3 bucket
Command: aws configure

Step 8: Install kubectl, refer to kubernetes documentation:
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

Make the kubectl binary executable.
chmod +x kubectl

Move file to /usr/local/bin

Step 9: Validate installation
kubectl --help

Step 10: Install KOPS followuing the kubernetes documentation:
https://kubernetes.io/docs/setup/production-environment/tools/kops/

Make the kops binary executable.
chmod +x kops-linux-amd64

Move the kops binary in to your PATH.
sudo mv kops-linux-amd64 /usr/local/bin/kops

Step 11: Set up cluster. See commands used

kops create cluster --name=kubedami.co.uk \
--state=s3://-kops --zones=us-east-1 \
--node-count=2 --node-size=t3.small --master-size=t3.small --dns-zone=kubedami.co.uk \
--node-volume-size=8 --master-volume-size=8

Step 11:Update and Validate CLuster

kops update cluster --name kubedami.lojucloud.co.uk --yes --admin --state=s3://vprofile-kops-damiloju

kops validate cluster --state=s3://vprofile-kops-damiloju

Step 12: Log on to AWS to see nodes created.

