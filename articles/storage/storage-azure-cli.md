---
title: "使用 Azure CLI 2.0 搭配 Azure 儲存體 | Microsoft Docs"
description: "了解如何使用「Azure 命令列介面」(Azure CLI) 2.0 搭配「Azure 儲存體」來建立和管理儲存體帳戶，以及處理 Azure Blob 和檔案。 Azure CLI 2.0 是一種以 Python 撰寫的跨平台工具。"
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 6098216f7dd901ea48fb3ab969c7934cc288b247
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-20-with-azure-storage"></a><span data-ttu-id="774f1-104">使用 Azure CLI 2.0 搭配 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="774f1-104">Using the Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="774f1-105">開放原始碼、跨平台的 Azure CLI 2.0 提供一組命令，供您運用在 Azure 平台上。</span><span class="sxs-lookup"><span data-stu-id="774f1-105">The open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with the Azure platform.</span></span> <span data-ttu-id="774f1-106">它提供許多與 [Azure 入口網站](https://portal.azure.com)相同的功能，包括豐富的資料存取功能。</span><span class="sxs-lookup"><span data-stu-id="774f1-106">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="774f1-107">在本指南中，我們會說明如何使用 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) 來執行數項工作，以便使用您的 Azure 儲存體帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="774f1-107">In this guide, we show you how to use the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to perform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="774f1-108">建議您在使用本指南之前，先下載並安裝或升級至最新版的 CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="774f1-108">We recommend that you download and install or upgrade to the latest version of the CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="774f1-109">本指南中的範例假設在 Ubuntu 上使用 Bash 殼層，但其他平台應以類似方式執行。</span><span class="sxs-lookup"><span data-stu-id="774f1-109">The examples in the guide assume the use of the Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="774f1-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="774f1-110">Prerequisites</span></span>
<span data-ttu-id="774f1-111">本指南假設您已了解 Azure 儲存體的基本概念。</span><span class="sxs-lookup"><span data-stu-id="774f1-111">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="774f1-112">而且假設您可以滿足針對 Azure 和儲存體服務所指定的帳戶建立需求。</span><span class="sxs-lookup"><span data-stu-id="774f1-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="774f1-113">帳戶</span><span class="sxs-lookup"><span data-stu-id="774f1-113">Accounts</span></span>
* <span data-ttu-id="774f1-114">**Azure 帳戶**：如果您沒有 Azure 訂用帳戶，請[建立免費的 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="774f1-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="774f1-115">**儲存體帳戶**：請參閱[關於 Azure 儲存體帳戶](../storage/storage-create-storage-account.md)中的[建立儲存體帳戶](../storage/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="774f1-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-the-azure-cli-20"></a><span data-ttu-id="774f1-116">安裝 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="774f1-116">Install the Azure CLI 2.0</span></span>

<span data-ttu-id="774f1-117">依照[安裝 Azure CLI 2.0](/cli/azure/install-az-cli2) 中的指示下載並安裝 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="774f1-117">Download and install the Azure CLI 2.0 by following the instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="774f1-118">如果您有安裝問題，請參閱本文的[安裝疑難排解](/cli/azure/install-az-cli2#installation-troubleshooting)一節，以及 GitHub 上的[安裝疑難排解](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md)指南。</span><span class="sxs-lookup"><span data-stu-id="774f1-118">If you have trouble with the installation, check out the [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of the article, and the [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-the-cli"></a><span data-ttu-id="774f1-119">使用 CLI</span><span class="sxs-lookup"><span data-stu-id="774f1-119">Working with the CLI</span></span>

<span data-ttu-id="774f1-120">安裝 CLI 之後，您即可在命令列介面 (Bash、終端機、命令提示字元) 中使用 `az` 命令，存取 Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="774f1-120">Once you've installed the CLI, you can use the `az` command in your command-line interface (Bash, Terminal, Command Prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="774f1-121">輸入 `az` 命令，以查看基底命令的完整清單 (下列輸出範例已截斷)︰</span><span class="sxs-lookup"><span data-stu-id="774f1-121">Type the `az` command to see a full list of the base commands (the following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome to the cool new Azure CLI!

Here are the base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="774f1-122">在命令列介面中，執行 `az storage --help` 命令以列出 `storage` 命令子群組。</span><span class="sxs-lookup"><span data-stu-id="774f1-122">In your command-line interface, execute the command `az storage --help` to list the `storage` command subgroups.</span></span> <span data-ttu-id="774f1-123">子群組的描述提供 Azure CLI 針對使用儲存體資源所提供的功能概觀。</span><span class="sxs-lookup"><span data-stu-id="774f1-123">The descriptions of the subgroups provide an overview of the functionality the Azure CLI provides for working with your storage resources.</span></span>

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use the standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues to effectively scale applications according to traffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-the-cli-to-your-azure-subscription"></a><span data-ttu-id="774f1-124">將 CLI 連接至您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="774f1-124">Connect the CLI to your Azure subscription</span></span>

<span data-ttu-id="774f1-125">若要使用 Azure 訂用帳戶中的資源，您必須先使用 `az login` 登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="774f1-125">To work with the resources in your Azure subscription, you must first log in to your Azure account with `az login`.</span></span> <span data-ttu-id="774f1-126">登入的方法有數種：</span><span class="sxs-lookup"><span data-stu-id="774f1-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="774f1-127">**互動式登入**：`az login`</span><span class="sxs-lookup"><span data-stu-id="774f1-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="774f1-128">**以使用者名稱和密碼登入**：`az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="774f1-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="774f1-129">這不適用於 Microsoft 帳戶或使用 Multi-Factor Authentication 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="774f1-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="774f1-130">**登入服務主體**：`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="774f1-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="774f1-131">Azure CLI 2.0 範例指令碼</span><span class="sxs-lookup"><span data-stu-id="774f1-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="774f1-132">接下來，我們將使用可發出一些基本 Azure CLI 2.0 命令的小型殼層指令碼，來與 Azure 儲存體資源問題互動。</span><span class="sxs-lookup"><span data-stu-id="774f1-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands to interact with Azure Storage resources.</span></span> <span data-ttu-id="774f1-133">指令碼會先在儲存體帳戶中建立新的容器，然後將現有的檔案 (以 blob 形式) 上傳至該容器。</span><span class="sxs-lookup"><span data-stu-id="774f1-133">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container.</span></span> <span data-ttu-id="774f1-134">它會接著列出容器中的所有 blob，最後，將此檔案下載至您指定的本機電腦上的目的地。</span><span class="sxs-lookup"><span data-stu-id="774f1-134">It then lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating the container..."
az storage container create --name $container_name

echo "Uploading the file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing the blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading the file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="774f1-135">**設定及執行指令碼**</span><span class="sxs-lookup"><span data-stu-id="774f1-135">**Configure and run the script**</span></span>

1. <span data-ttu-id="774f1-136">開啟您喜愛的文字編輯器，然後複製上述指令碼並貼入編輯器中。</span><span class="sxs-lookup"><span data-stu-id="774f1-136">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>

2. <span data-ttu-id="774f1-137">接下來，更新指令碼的變數以反映您的組態設定。</span><span class="sxs-lookup"><span data-stu-id="774f1-137">Next, update the script's variables to reflect your configuration settings.</span></span> <span data-ttu-id="774f1-138">依照指定取代下列值：</span><span class="sxs-lookup"><span data-stu-id="774f1-138">Replace the following values as specified:</span></span>

   * <span data-ttu-id="774f1-139">**\<storage_account_name\>**：您儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="774f1-139">**\<storage_account_name\>** The name of your storage account.</span></span>
   * <span data-ttu-id="774f1-140">**\<storage_account_key\>**：儲存體帳戶的主要或次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="774f1-140">**\<storage_account_key\>** The primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="774f1-141">**\<container_name\>**：要建立的新容器名稱，例如 "azure-cli-sample-container"。</span><span class="sxs-lookup"><span data-stu-id="774f1-141">**\<container_name\>** A name the new container to create, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="774f1-142">**\<blob_name\>**：容器中目的地 blob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="774f1-142">**\<blob_name\>** A name for the destination blob in the container.</span></span>
   * <span data-ttu-id="774f1-143">**\<file_to_upload\>**：本機電腦上小檔案的路徑，例如 "~/images/HelloWorld.png"。</span><span class="sxs-lookup"><span data-stu-id="774f1-143">**\<file_to_upload\>** The path to small file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="774f1-144">**\<destination_file\>**：目的地檔案路徑，例如 "~/downloadedImage.png"。</span><span class="sxs-lookup"><span data-stu-id="774f1-144">**\<destination_file\>** The destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="774f1-145">在您更新必要變數之後，請儲存指令碼並結束編輯器。</span><span class="sxs-lookup"><span data-stu-id="774f1-145">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="774f1-146">後續步驟假設您已將指令碼命名為 **my_storage_sample.sh**。</span><span class="sxs-lookup"><span data-stu-id="774f1-146">The next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="774f1-147">如有必要，請將指令碼標示為可執行檔︰`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="774f1-147">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="774f1-148">執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="774f1-148">Execute the script.</span></span> <span data-ttu-id="774f1-149">例如，在 Bash 中：`./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="774f1-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="774f1-150">您應該會看到類似下列的輸出，而您在指令碼中指定的 **\<destination_file\>** 應出現在您的本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="774f1-150">You should see output similar to the following, and the **\<destination_file\>** you specified in the script should appear on your local computer.</span></span>

```
Creating the container...
{
  "created": true
}
Uploading the file...
Percent complete: %100.0
Listing the blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading the file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="774f1-151">上述輸出採用**資料表**格式。</span><span class="sxs-lookup"><span data-stu-id="774f1-151">The preceding output is in **table** format.</span></span> <span data-ttu-id="774f1-152">您可以在 CLI 命令中指定 `--output` 引數，或使用 `az configure` 進行全域設定，以指定要使用哪一種輸出格式。</span><span class="sxs-lookup"><span data-stu-id="774f1-152">You can specify which output format to use by specifying the `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="774f1-153">管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="774f1-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="774f1-154">建立新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="774f1-154">Create a new storage account</span></span>
<span data-ttu-id="774f1-155">若要使用 Azure 儲存體，您需要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="774f1-155">To use Azure Storage, you need a storage account.</span></span> <span data-ttu-id="774f1-156">設定電腦以[連接至您的訂用帳戶](#connect-to-your-azure-subscription)之後，您可以建立新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="774f1-156">You can create a new Azure Storage account after you've configured your computer to [connect to your subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="774f1-157">`--location` [必要]：位置。</span><span class="sxs-lookup"><span data-stu-id="774f1-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="774f1-158">例如，「美國西部」。</span><span class="sxs-lookup"><span data-stu-id="774f1-158">For example, "West US".</span></span>
* <span data-ttu-id="774f1-159">`--name` [必要]：儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="774f1-159">`--name` [Required]: The storage account name.</span></span> <span data-ttu-id="774f1-160">名稱長度必須為 3-24 個字元，而且僅使用小寫英數字元。</span><span class="sxs-lookup"><span data-stu-id="774f1-160">The name must be 3 to 24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="774f1-161">`--resource-group` [必要]：資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="774f1-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="774f1-162">`--sku` [必要]：儲存體帳戶 SKU。</span><span class="sxs-lookup"><span data-stu-id="774f1-162">`--sku` [Required]: The storage account SKU.</span></span> <span data-ttu-id="774f1-163">允許的值：</span><span class="sxs-lookup"><span data-stu-id="774f1-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="774f1-164">設定預設 Azure 儲存體帳戶環境變數</span><span class="sxs-lookup"><span data-stu-id="774f1-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="774f1-165">您可以在 Azure 訂用帳戶中有多個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="774f1-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="774f1-166">若要選取其中一個來用於所有後續的儲存體命令，您可以設定下列環境變數︰</span><span class="sxs-lookup"><span data-stu-id="774f1-166">To select one of them to use for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="774f1-167">另一種設定預設儲存體帳戶的方法是使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="774f1-167">Another way to set a default storage account is by using a connection string.</span></span> <span data-ttu-id="774f1-168">首先，透過 `show-connection-string` 命令取得連接字串︰</span><span class="sxs-lookup"><span data-stu-id="774f1-168">First, get the connection string with the `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="774f1-169">然後複製輸出連接字串，並將它設定為 `AZURE_STORAGE_CONNECTION_STRING` 環境變數 (您可能需要用引號括住連接字串)：</span><span class="sxs-lookup"><span data-stu-id="774f1-169">Then copy the output connection string and set the `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need to enclose the connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="774f1-170">本文下列各節中的所有範例都假設您已設定 `AZURE_STORAGE_ACCOUNT` 和 `AZURE_STORAGE_ACCESS_KEY` 環境變數。</span><span class="sxs-lookup"><span data-stu-id="774f1-170">All examples in the following sections of this article assume that you've set the `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="774f1-171">建立和管理 Blob</span><span class="sxs-lookup"><span data-stu-id="774f1-171">Create and manage blobs</span></span>
<span data-ttu-id="774f1-172">Azure Blob 儲存體是一項儲存大量非結構化資料的服務 (例如文字或二進位資料)，全球任何地方都可透過 HTTP 或 HTTPS 來存取這些資料。</span><span class="sxs-lookup"><span data-stu-id="774f1-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="774f1-173">本節假設您已熟悉 Azure Blob 儲存體的概念。</span><span class="sxs-lookup"><span data-stu-id="774f1-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="774f1-174">如需詳細資訊，請參閱[使用 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md)和 [Blob 服務概念](/rest/api/storageservices/blob-service-concepts)。</span><span class="sxs-lookup"><span data-stu-id="774f1-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="774f1-175">建立容器</span><span class="sxs-lookup"><span data-stu-id="774f1-175">Create a container</span></span>
<span data-ttu-id="774f1-176">Azure 儲存體中的每個 Blob 必須位於一個容器中。</span><span class="sxs-lookup"><span data-stu-id="774f1-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="774f1-177">您可以使用 `az storage container create` 命令來建立容器：</span><span class="sxs-lookup"><span data-stu-id="774f1-177">You can create a container by using the `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="774f1-178">您可以指定選擇性 `--public-access` 引數，以針對新容器設定讀取權限的三個層級之一︰</span><span class="sxs-lookup"><span data-stu-id="774f1-178">You can set one of three levels of read access for a new container by specifying the optional  `--public-access` argument:</span></span>

* <span data-ttu-id="774f1-179">`off` (預設值)︰容器資料為帳戶擁有者私有。</span><span class="sxs-lookup"><span data-stu-id="774f1-179">`off` (default): Container data is private to the account owner.</span></span>
* <span data-ttu-id="774f1-180">`blob`：Blob 的公用讀取權限。</span><span class="sxs-lookup"><span data-stu-id="774f1-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="774f1-181">`container`︰整個容器的公用讀取和清單權限。</span><span class="sxs-lookup"><span data-stu-id="774f1-181">`container`: Public read and list access to the entire container.</span></span>

<span data-ttu-id="774f1-182">如需詳細資訊，請參閱 [管理對容器與 Blob 的匿名讀取權限](storage-manage-access-to-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="774f1-182">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-to-a-container"></a><span data-ttu-id="774f1-183">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="774f1-183">Upload a blob to a container</span></span>
<span data-ttu-id="774f1-184">Azure Blob 儲存體支援區塊、附加和分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="774f1-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="774f1-185">使用 `blob upload` 命令將 blob 上傳至容器：</span><span class="sxs-lookup"><span data-stu-id="774f1-185">Upload blobs to a container by using the `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="774f1-186">根據預設，`blob upload` 命令會將 *.vhd 檔案上傳至分頁 blob 或者區塊 blob。</span><span class="sxs-lookup"><span data-stu-id="774f1-186">By default, the `blob upload` command uploads *.vhd files to page blobs, or block blobs otherwise.</span></span> <span data-ttu-id="774f1-187">若要在上傳 blob 時指定另一種類型，您可以使用 `--type` 引數 - 允許的值為 `append`、`block` 和 `page`。</span><span class="sxs-lookup"><span data-stu-id="774f1-187">To specify another type when you upload a blob, you can use the `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="774f1-188">如需不同 Blob 類型的詳細資訊，請參閱[了解區塊 Blob、附加 Blob 及分頁 Blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs)。</span><span class="sxs-lookup"><span data-stu-id="774f1-188">For more information on the different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="774f1-189">從容器下載 Blob</span><span class="sxs-lookup"><span data-stu-id="774f1-189">Download a blob from a container</span></span>
<span data-ttu-id="774f1-190">此範例示範如何從容器下載 Blob：</span><span class="sxs-lookup"><span data-stu-id="774f1-190">This example demonstrates how to download a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="774f1-191">列出容器中的 Blob</span><span class="sxs-lookup"><span data-stu-id="774f1-191">List the blobs in a container</span></span>

<span data-ttu-id="774f1-192">使用 [az storage blob list](/cli/azure/storage/blob#list) 命令列出容器中的 blob。</span><span class="sxs-lookup"><span data-stu-id="774f1-192">List the blobs in a container with the [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="774f1-193">複製 Blob</span><span class="sxs-lookup"><span data-stu-id="774f1-193">Copy blobs</span></span>
<span data-ttu-id="774f1-194">您可以在儲存體帳戶內或在不同儲存體帳戶和區域之間，以非同步方式複製 Blob。</span><span class="sxs-lookup"><span data-stu-id="774f1-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="774f1-195">下列範例示範如何從一個儲存體帳戶複製 Blob 到另一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="774f1-195">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="774f1-196">我們會先在來源儲存體帳戶中建立容器，指定對其 Blob 的公用讀取存取權。</span><span class="sxs-lookup"><span data-stu-id="774f1-196">We first create a container in the source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="774f1-197">接著，我們會將檔案上傳至容器，最後，將 Blob 從該容器複製到目的地儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="774f1-197">Next, we upload a file to the container, and finally, copy the blob from that container into a container in the destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob to container in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account to destination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="774f1-198">在上面的範例中，目的地容器必須已存在於目的地儲存體帳戶中，複製作業才能成功。</span><span class="sxs-lookup"><span data-stu-id="774f1-198">In the above example, the destination container must already exist in the destination storage account for the copy operation to succeed.</span></span> <span data-ttu-id="774f1-199">此外，在 `--source-uri` 引數中指定的來源 Blob 必須包含共用存取簽章 (SAS) 權杖，或者可公開存取，如此範例所示。</span><span class="sxs-lookup"><span data-stu-id="774f1-199">Additionally, the source blob specified in the `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="774f1-200">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="774f1-200">Delete a blob</span></span>
<span data-ttu-id="774f1-201">若要刪除 Blob，請使用 `blob delete` 命令：</span><span class="sxs-lookup"><span data-stu-id="774f1-201">To delete a blob, use the `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="774f1-202">建立和管理檔案共用</span><span class="sxs-lookup"><span data-stu-id="774f1-202">Create and manage file shares</span></span>
<span data-ttu-id="774f1-203">Azure 檔案儲存體為使用伺服器訊息區 (SMB) 通訊協定的應用程式提供共用儲存體。</span><span class="sxs-lookup"><span data-stu-id="774f1-203">Azure File storage offers shared storage for applications using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="774f1-204">Microsoft Azure 虛擬機器和雲端服務，以及內部部署應用程式，可以透過掛接共用，共用檔案資料。</span><span class="sxs-lookup"><span data-stu-id="774f1-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="774f1-205">您可以透過 Azure CLI 管理檔案共用和檔案資料。</span><span class="sxs-lookup"><span data-stu-id="774f1-205">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="774f1-206">如需 Azure 檔案儲存體的詳細資訊，請參閱[在 Windows 上開始使用 Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)或[如何搭配 Linux 使用 Azure 檔案儲存體](storage-how-to-use-files-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="774f1-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="774f1-207">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="774f1-207">Create a file share</span></span>
<span data-ttu-id="774f1-208">Azure 檔案共用是 Azure 中的 SMB 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="774f1-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="774f1-209">所有目錄和檔案都必須在檔案共用中建立。</span><span class="sxs-lookup"><span data-stu-id="774f1-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="774f1-210">帳戶可包含無限制數目的共用，而共用可儲存無限制數目的檔案，最多可達儲存體帳戶的容量限制。</span><span class="sxs-lookup"><span data-stu-id="774f1-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="774f1-211">下列範例會建立名為 **myshare** 的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="774f1-211">The following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="774f1-212">建立目錄</span><span class="sxs-lookup"><span data-stu-id="774f1-212">Create a directory</span></span>
<span data-ttu-id="774f1-213">目錄會提供 Azure 檔案共用的階層式結構。</span><span class="sxs-lookup"><span data-stu-id="774f1-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="774f1-214">下列範例會在檔案共用中建立名為 **myDir** 的目錄。</span><span class="sxs-lookup"><span data-stu-id="774f1-214">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="774f1-215">目錄路徑可包含多個層級，例如 **dir1/dir2**。</span><span class="sxs-lookup"><span data-stu-id="774f1-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="774f1-216">不過，您必須先確定所有父目錄都存在，才能建立子目錄。</span><span class="sxs-lookup"><span data-stu-id="774f1-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="774f1-217">例如，如果路徑是 **dir1/dir2**，您必須先建立目錄 **dir1**，然後再建立目錄 **dir2**。</span><span class="sxs-lookup"><span data-stu-id="774f1-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-to-a-share"></a><span data-ttu-id="774f1-218">將本機檔案上傳至共用</span><span class="sxs-lookup"><span data-stu-id="774f1-218">Upload a local file to a share</span></span>
<span data-ttu-id="774f1-219">下列範例會將檔案從 **~/temp/samplefile.txt** 上傳至 **myshare** 檔案共用的根目錄。</span><span class="sxs-lookup"><span data-stu-id="774f1-219">The following example uploads a file from **~/temp/samplefile.txt** to root of the **myshare** file share.</span></span> <span data-ttu-id="774f1-220">`--source` 引數會指定要上傳的現有本機檔案。</span><span class="sxs-lookup"><span data-stu-id="774f1-220">The `--source` argument specifies the existing local file to upload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="774f1-221">建立目錄時，您可以指定共用中的目錄路徑，以將檔案上傳至共用中的現有目錄︰</span><span class="sxs-lookup"><span data-stu-id="774f1-221">As with directory creation, you can specify a directory path within the share to upload the file to an existing directory within the share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="774f1-222">共用中的檔案大小可能高達 1 TB。</span><span class="sxs-lookup"><span data-stu-id="774f1-222">A file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-a-share"></a><span data-ttu-id="774f1-223">列出共用中的檔案</span><span class="sxs-lookup"><span data-stu-id="774f1-223">List the files in a share</span></span>
<span data-ttu-id="774f1-224">您可以使用 `az storage file list` 命令列出共用中的檔案和目錄︰</span><span class="sxs-lookup"><span data-stu-id="774f1-224">You can list files and directories in a share by using the `az storage file list` command:</span></span>

```azurecli
# List the files in the root of a share
az storage file list --share-name myshare --output table

# List the files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List the files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="774f1-225">複製檔案</span><span class="sxs-lookup"><span data-stu-id="774f1-225">Copy files</span></span>      
<span data-ttu-id="774f1-226">您可以將檔案複製到另一個檔案、將檔案複製到 Blob 或將 Blob 複製到檔案。</span><span class="sxs-lookup"><span data-stu-id="774f1-226">You can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="774f1-227">例如，若要將檔案複製到不同共用中的目錄︰</span><span class="sxs-lookup"><span data-stu-id="774f1-227">For example, to copy a file to a directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="774f1-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="774f1-228">Next steps</span></span>
<span data-ttu-id="774f1-229">以下有一些額外的資源，可供深入了解如何使用 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="774f1-229">Here are some additional resources for learning more about working with the Azure CLI 2.0.</span></span>

* [<span data-ttu-id="774f1-230">開始使用 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="774f1-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="774f1-231">Azure CLI 2.0 命令參考</span><span class="sxs-lookup"><span data-stu-id="774f1-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="774f1-232">GitHub 上的 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="774f1-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
