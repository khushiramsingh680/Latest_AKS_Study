+++
title = "Kubernetes Installation"
type = "chapter"
weight = 2
+++

# Azure AKS Cluster Creation Script

## Step 1: Login with Service Principal

```bash
az login \
  --service-principal \
  -t <Tenant-ID> \
  -u <Client-ID> \
  -p <Client-secret>
```

## Step 2: Set Subscription

```bash
az account set -s <subscription-id>

```

## Step 3: Set Environment Variables

```bash
export RANDOM_ID="$(openssl rand -hex 3)"
export MY_RESOURCE_GROUP_NAME="rg-aks$RANDOM_ID"
export REGION="westeurope"
export MY_AKS_CLUSTER_NAME="aks$RANDOM_ID"
export MY_DNS_LABEL="mydnslabel$RANDOM_ID"
```

## Step 4: Create Resource Group

```bash
az group create --name $MY_RESOURCE_GROUP_NAME --location $REGION
```

## Step 5: Create AKS cluster

```bash
az aks create \
  --resource-group $MY_RESOURCE_GROUP_NAME \
  --name $MY_AKS_CLUSTER_NAME \
  --node-count 1 \
  --node-vm-size standard_d2s_v5
```

