# Azure ML Datastore Setup

This guide provides CLI commands to create a datastore inside your Azure Machine Learning workspace.
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
    ```

    Replace the placeholders with your actual values:
    - `<storage-account-name>`: Name of the storage account you want to create.
    - `<resource-group>`: Name of your resource group.
    - `<location>`: Azure region for the storage account.

3. **Create a container in the storage account:**

    ```sh
    az storage container create --name <container-name> \
        --account-name <storage-account-name>
    ```

    Replace the placeholders with your actual values:
    - `<container-name>`: Name of the container you want to create.
    - `<storage-account-name>`: Name of your storage account.
## Prerequisites

- Azure CLI installed
- Azure Machine Learning CLI extension installed
- Logged into your Azure account
- An existing Azure Machine Learning workspace

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
    az ml datastore create --name <datastore-name> \
        --workspace-name <workspace-name> \
        --resource-group <resource-group> \
        --account-name <storage-account-name> \
        --container-name <container-name> \
        --type <datastore-type> \
        --account-key <storage-account-key>
    ```

    Replace the placeholders with your actual values:
    - `<datastore-name>`: Name of the datastore you want to create.
    - `<workspace-name>`: Name of your Azure ML workspace.
    - `<resource-group>`: Resource group of your Azure ML workspace.
    - `<storage-account-name>`: Name of your Azure storage account.
    - `<container-name>`: Name of the container in your storage account.
    - `<datastore-type>`: Type of the datastore (e.g., `AzureBlob`, `AzureFile`).
    - `<storage-account-key>`: Access key for your storage account.

## Example

```sh
az ml datastore create --name mydatastore \
    --workspace-name myworkspace \
    --resource-group myresourcegroup \
    --account-name mystorageaccount \
    --container-name mycontainer \
    --type AzureBlob \
    --account-key myaccountkey
```

## Verification

To verify that the datastore has been created, you can list all datastores in your workspace:

```sh
az ml datastore list --workspace-name <workspace-name> --resource-group <resource-group>
```

Replace `<workspace-name>` and `<resource-group>` with your actual values.

## Additional Resources

- [Azure Machine Learning CLI Documentation](https://docs.microsoft.com/en-us/azure/machine-learning/reference-azure-machine-learning-cli)
