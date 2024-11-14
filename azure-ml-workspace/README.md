# Azure ML CLI Setup Guide

This guide walks you through setting up the Azure CLI environment with the necessary extensions for working with Azure Machine Learning.

## Prerequisites

- Ensure you have [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) installed on your local machine.

## Check Azure CLI Version

Verify the Azure CLI version to ensure compatibility with the latest extensions.

```bash
az version

# Remove the old Azure Machine Learning CLI extensions
az extension remove -n azure-cli-ml
az extension remove -n ml

# Install the ml extension
az extension add -n ml -y

# Login to Azure
az login

# Set the subscription ID for the Azure resources you intend to work with. Replace xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx with your actual subscription ID.

az account set --subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

# Create a Resource Group
az group create --name azmlops-dev-rg --location eastus2


# Create an Azure ML Workspace
az ml workspace create -n azmlopscli-ws -g azmlops-dev-rg -l eastus2

```