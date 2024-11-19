# Azure ML Datastore Setup

This guide provides CLI commands to create a datastore inside your Azure Machine Learning workspace.

## Prerequisites

- Azure CLI installed
- Azure Machine Learning CLI extension installed
- Logged into your Azure account
- An existing Azure Machine Learning workspace

## Create a Storage Account

Before creating a datastore, you need to have a storage account. Here are the steps to create one:

1. **Create a resource group (if you don't have one):**

    ```sh
    az group create --name <resource-group> --location <location>
    ```

    Replace `<resource-group>` with the name of your resource group and `<location>` with the Azure region you want to use.

2. **Create a storage account:**

    ```sh
    az storage account create --name <storage-account-name> \
        --resource-group <resource-group> \
        --location <location> \
        --sku Standard_LRS

     az storage account create --name pythonsademo99823 \
        --resource-group section-2-handson \
        --location eastus \
        --sku Standard_LRS
    ```

    Replace the placeholders with your actual values:
    - `<storage-account-name>`: Name of the storage account you want to create.
    - `<resource-group>`: Name of your resource group.
    - `<location>`: Azure region for the storage account.

3. **Create a container in the storage account:**

    ```sh
    az storage container create --name <container-name> \
        --account-name <storage-account-name>
    
    az storage container create --name mycontainer \
        --account-name pythonsademo99823
    ```

    Replace the placeholders with your actual values:
    - `<container-name>`: Name of the container you want to create.
    - `<storage-account-name>`: Name of your storage account.

## Steps to Create a Datastore

1. **Login to Azure:**

    ```sh
    az login
    ```

2. **Set the subscription:**

    ```sh
    az account set --subscription <your-subscription-id>
    ```

3. **Create a new datastore:**

    ```sh
    az ml datastore create --file blobstore.yml --resource-group <resource-group> --workspace-name <workspace-name>

    az ml datastore create --file blobstore.yml --resource-group section-2-handson --workspace-name section2

    ```

    Replace the placeholders with your actual values:
    - `<datastore-name>`: Name of the datastore you want to create.
    - `<workspace-name>`: Name of your Azure ML workspace.
    - `<resource-group>`: Resource group of your Azure ML workspace.
    - `<storage-account-name>`: Name of your Azure storage account.
    - `<container-name>`: Name of the container in your storage account.
    - `<datastore-type>`: Type of the datastore (e.g., `AzureBlob`, `AzureFile`).
    - `<storage-account-key>`: Access key for your storage account.

```
## Example Configuration File

Create a configuration file named `blobstore.yml` with the following content:

```yaml
$schema: https://azuremlschemas.azureedge.net/latest/datastore.schema.json
name: <datastore-name>
description: Datastore for Azure ML
type: <datastore-type>
account_name: <storage-account-name>
container_name: <container-name>
credentials:
    account_key: <storage-account-key>
```

Replace the placeholders with your actual values:
- `<datastore-name>`: Name of the datastore you want to create.
- `<datastore-type>`: Type of the datastore (e.g., `AzureBlob`, `AzureFile`).
- `<storage-account-name>`: Name of your Azure storage account.
- `<container-name>`: Name of the container in your storage account.
- `<storage-account-key>`: Access key for your storage account.

## Verify Datastore

To verify that the datastore has been created successfully, use the following command:

```sh
az ml datastore show --name <datastore-name> --resource-group <resource-group> --workspace-name <workspace-name>
```

Replace the placeholders with your actual values:
- `<datastore-name>`: Name of the datastore you created.
- `<resource-group>`: Resource group of your Azure ML workspace.
- `<workspace-name>`: Name of your Azure ML workspace.

## Additional Resources

- [Azure Machine Learning CLI Documentation](https://docs.microsoft.com/en-us/azure/machine-learning/reference-azure-machine-learning-cli)
