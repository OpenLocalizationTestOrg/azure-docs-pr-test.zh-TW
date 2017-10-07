---
title: "aaaUsing hello 與 Azure 儲存體的 Azure CLI 2.0 |Microsoft 文件"
description: "了解 toouse hello Azure 命令列介面 (Azure CLI) 2.0 與 Azure 儲存體 toocreate 和管理儲存體帳戶和使用 Azure blob 及檔案的方式。 hello Azure CLI 2.0 是以 Python 撰寫的跨平台工具。"
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
ms.openlocfilehash: 14e6eb0c913676380c90a72563276245e7f08aa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a><span data-ttu-id="c8190-104">使用 Azure CLI 2.0 hello 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="c8190-104">Using hello Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="c8190-105">hello 開放原始碼、 跨平台 Azure CLI 2.0 提供一組命令使用 hello Azure 平台。</span><span class="sxs-lookup"><span data-stu-id="c8190-105">hello open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with hello Azure platform.</span></span> <span data-ttu-id="c8190-106">它可提供許多相同的功能位於 hello hello [Azure 入口網站](https://portal.azure.com)，包括豐富的資料存取。</span><span class="sxs-lookup"><span data-stu-id="c8190-106">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="c8190-107">在本指南中，我們會示範如何 toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform 幾項工作使用您的 Azure 儲存體帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="c8190-107">In this guide, we show you how toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="c8190-108">我們建議您下載並安裝或升級使用本指南之前的 hello CLI 2.0 toohello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="c8190-108">We recommend that you download and install or upgrade toohello latest version of hello CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="c8190-109">hello 指南中的 hello 範例假設 hello hello Bash 殼層 Ubuntu 上, 使用，但其他平台應該同樣地執行。</span><span class="sxs-lookup"><span data-stu-id="c8190-109">hello examples in hello guide assume hello use of hello Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="c8190-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c8190-110">Prerequisites</span></span>
<span data-ttu-id="c8190-111">本指南假設您已了解 hello 的 Azure 儲存體的基本概念。</span><span class="sxs-lookup"><span data-stu-id="c8190-111">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="c8190-112">它也假設您使用的是可以 toosatisfy hello 帳戶建立需求下方指定的 Azure 與 hello 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="c8190-112">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="c8190-113">帳戶</span><span class="sxs-lookup"><span data-stu-id="c8190-113">Accounts</span></span>
* <span data-ttu-id="c8190-114">**Azure 帳戶**：如果您沒有 Azure 訂用帳戶，請[建立免費的 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="c8190-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="c8190-115">**儲存體帳戶**：請參閱[關於 Azure 儲存體帳戶](storage-create-storage-account.md)中的[建立儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="c8190-115">**Storage account**: See [Create a storage account](storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](storage-create-storage-account.md).</span></span>

### <a name="install-hello-azure-cli-20"></a><span data-ttu-id="c8190-116">安裝 hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c8190-116">Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="c8190-117">下載並安裝 hello 指示中所述的 hello Azure CLI 2.0[安裝 Azure CLI 2.0](/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="c8190-117">Download and install hello Azure CLI 2.0 by following hello instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="c8190-118">如果您有 hello 安裝問題，請參閱 hello[安裝疑難排解](/cli/azure/install-az-cli2#installation-troubleshooting)hello 文件： hello 的區段[安裝疑難排解](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md)GitHub 上的指南。</span><span class="sxs-lookup"><span data-stu-id="c8190-118">If you have trouble with hello installation, check out hello [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of hello article, and hello [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-hello-cli"></a><span data-ttu-id="c8190-119">使用 CLI hello</span><span class="sxs-lookup"><span data-stu-id="c8190-119">Working with hello CLI</span></span>

<span data-ttu-id="c8190-120">一旦您已安裝 hello CLI，您可以使用 hello`az`命令 Bash、 終端機 （命令提示字元） 的命令列介面 tooaccess hello Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="c8190-120">Once you've installed hello CLI, you can use hello `az` command in your command-line interface (Bash, Terminal, Command Prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="c8190-121">型別 hello`az`命令 toosee hello （下列範例輸出的 hello 已截斷） 的基底命令的完整清單：</span><span class="sxs-lookup"><span data-stu-id="c8190-121">Type hello `az` command toosee a full list of hello base commands (hello following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="c8190-122">在命令列介面中，執行 hello 命令`az storage --help`toolist hello`storage`命令子群組。</span><span class="sxs-lookup"><span data-stu-id="c8190-122">In your command-line interface, execute hello command `az storage --help` toolist hello `storage` command subgroups.</span></span> <span data-ttu-id="c8190-123">hello 描述 hello 子群組提供 hello 功能 hello Azure CLI 提供使用儲存體資源的概觀。</span><span class="sxs-lookup"><span data-stu-id="c8190-123">hello descriptions of hello subgroups provide an overview of hello functionality hello Azure CLI provides for working with your storage resources.</span></span>

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
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a><span data-ttu-id="c8190-124">連接 hello CLI tooyour Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c8190-124">Connect hello CLI tooyour Azure subscription</span></span>

<span data-ttu-id="c8190-125">與您 Azure 訂用帳戶中的 hello 資源 toowork，您必須先登入 tooyour Azure 帳戶`az login`。</span><span class="sxs-lookup"><span data-stu-id="c8190-125">toowork with hello resources in your Azure subscription, you must first log in tooyour Azure account with `az login`.</span></span> <span data-ttu-id="c8190-126">登入的方法有數種：</span><span class="sxs-lookup"><span data-stu-id="c8190-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="c8190-127">**互動式登入**：`az login`</span><span class="sxs-lookup"><span data-stu-id="c8190-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="c8190-128">**以使用者名稱和密碼登入**：`az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="c8190-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="c8190-129">這不適用於 Microsoft 帳戶或使用 Multi-Factor Authentication 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c8190-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="c8190-130">**登入服務主體**：`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="c8190-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="c8190-131">Azure CLI 2.0 範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c8190-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="c8190-132">接下來，我們將使用一些基本 Azure CLI 2.0 命令 toointeract 發出與 Azure 儲存體資源的小型的殼層指令碼。</span><span class="sxs-lookup"><span data-stu-id="c8190-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands toointeract with Azure Storage resources.</span></span> <span data-ttu-id="c8190-133">hello 指令碼會先在儲存體帳戶中建立新的容器，然後上傳現有的檔案 （以 blob 的形式） toothat 容器。</span><span class="sxs-lookup"><span data-stu-id="c8190-133">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container.</span></span> <span data-ttu-id="c8190-134">它接著會列出 hello 容器中的所有 blob，和最後，下載 hello 檔案 tooa 目的地，您指定在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="c8190-134">It then lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="c8190-135">**設定及執行 hello 指令碼**</span><span class="sxs-lookup"><span data-stu-id="c8190-135">**Configure and run hello script**</span></span>

1. <span data-ttu-id="c8190-136">開啟您偏好的文字編輯器 中，然後複製並貼到 hello 編輯器上述指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="c8190-136">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>

2. <span data-ttu-id="c8190-137">接著，更新 hello 指令碼變數 tooreflect 組態設定。</span><span class="sxs-lookup"><span data-stu-id="c8190-137">Next, update hello script's variables tooreflect your configuration settings.</span></span> <span data-ttu-id="c8190-138">取代為下列指定的值的 hello:</span><span class="sxs-lookup"><span data-stu-id="c8190-138">Replace hello following values as specified:</span></span>

   * <span data-ttu-id="c8190-139">**\<storage_account_name\>**  hello 您的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="c8190-139">**\<storage_account_name\>** hello name of your storage account.</span></span>
   * <span data-ttu-id="c8190-140">**\<storage_account_key\>**  hello 儲存體帳戶的主要或次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8190-140">**\<storage_account_key\>** hello primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="c8190-141">**\<container_name\>** 名稱 hello 新容器 toocreate，例如"azure cli-範例-容器 」。</span><span class="sxs-lookup"><span data-stu-id="c8190-141">**\<container_name\>** A name hello new container toocreate, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="c8190-142">**\<blob_name\>**  hello 容器中的 hello 目的地 blob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="c8190-142">**\<blob_name\>** A name for hello destination blob in hello container.</span></span>
   * <span data-ttu-id="c8190-143">**\<file_to_upload\>**  hello 路徑 toosmall 檔案儲存在本機電腦，例如"~ / images/HelloWorld.png"。</span><span class="sxs-lookup"><span data-stu-id="c8190-143">**\<file_to_upload\>** hello path toosmall file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="c8190-144">**\<destination_file\>**  hello 目的地檔案路徑，例如"~ / downloadedImage.png"。</span><span class="sxs-lookup"><span data-stu-id="c8190-144">**\<destination_file\>** hello destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="c8190-145">更新 hello 必要變數之後，儲存 hello 指令碼，並結束編輯器。</span><span class="sxs-lookup"><span data-stu-id="c8190-145">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="c8190-146">hello 接下來的步驟假設您已命名為您的指令碼**my_storage_sample.sh**。</span><span class="sxs-lookup"><span data-stu-id="c8190-146">hello next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="c8190-147">如有必要，請標示 hello 做為可執行檔的指令碼：`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="c8190-147">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="c8190-148">執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="c8190-148">Execute hello script.</span></span> <span data-ttu-id="c8190-149">例如，在 Bash 中：`./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="c8190-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="c8190-150">您應看到類似 toohello 下列程式碼輸出，及 hello  **\<destination_file\>**  hello 中所指定指令碼應該會出現在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="c8190-150">You should see output similar toohello following, and hello **\<destination_file\>** you specified in hello script should appear on your local computer.</span></span>

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="c8190-151">hello 上述輸出會**資料表**格式。</span><span class="sxs-lookup"><span data-stu-id="c8190-151">hello preceding output is in **table** format.</span></span> <span data-ttu-id="c8190-152">您可以指定哪一個輸出格式 toouse 藉由指定 hello`--output`在 CLI 命令中的引數，或將它全域使用`az configure`。</span><span class="sxs-lookup"><span data-stu-id="c8190-152">You can specify which output format toouse by specifying hello `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="c8190-153">管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c8190-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="c8190-154">建立新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c8190-154">Create a new storage account</span></span>
<span data-ttu-id="c8190-155">toouse Azure 儲存體，您需要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c8190-155">toouse Azure Storage, you need a storage account.</span></span> <span data-ttu-id="c8190-156">您可以建立新的 Azure 儲存體帳戶之後您已設定您的電腦太,[連接 tooyour 訂閱](#connect-to-your-azure-subscription)。</span><span class="sxs-lookup"><span data-stu-id="c8190-156">You can create a new Azure Storage account after you've configured your computer too[connect tooyour subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="c8190-157">`--location` [必要]：位置。</span><span class="sxs-lookup"><span data-stu-id="c8190-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="c8190-158">例如，「美國西部」。</span><span class="sxs-lookup"><span data-stu-id="c8190-158">For example, "West US".</span></span>
* <span data-ttu-id="c8190-159">`--name`[必要]: hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="c8190-159">`--name` [Required]: hello storage account name.</span></span> <span data-ttu-id="c8190-160">hello 名稱必須 3 too24 個字元的長度，且只使用小寫英數字元。</span><span class="sxs-lookup"><span data-stu-id="c8190-160">hello name must be 3 too24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="c8190-161">`--resource-group` [必要]：資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="c8190-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="c8190-162">`--sku`[必要]: hello SKU 的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c8190-162">`--sku` [Required]: hello storage account SKU.</span></span> <span data-ttu-id="c8190-163">允許的值：</span><span class="sxs-lookup"><span data-stu-id="c8190-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="c8190-164">設定預設 Azure 儲存體帳戶環境變數</span><span class="sxs-lookup"><span data-stu-id="c8190-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="c8190-165">您可以在 Azure 訂用帳戶中有多個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c8190-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="c8190-166">其中一個 tooselect 所有後續的存放裝置的 toouse 命令，您可以設定這些環境變數：</span><span class="sxs-lookup"><span data-stu-id="c8190-166">tooselect one of them toouse for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="c8190-167">另一個方式 tooset 預設儲存體帳戶是使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="c8190-167">Another way tooset a default storage account is by using a connection string.</span></span> <span data-ttu-id="c8190-168">首先，取得 hello 連接字串以 hello`show-connection-string`命令：</span><span class="sxs-lookup"><span data-stu-id="c8190-168">First, get hello connection string with hello `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="c8190-169">複製 hello 輸出連接字串，然後設定 hello `AZURE_STORAGE_CONNECTION_STRING` （您可能需要以引號括住 tooenclose hello 連接字串） 的環境變數：</span><span class="sxs-lookup"><span data-stu-id="c8190-169">Then copy hello output connection string and set hello `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need tooenclose hello connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="c8190-170">Hello 下列各節的這篇文章中的所有範例都假設您已設定 hello`AZURE_STORAGE_ACCOUNT`和`AZURE_STORAGE_ACCESS_KEY`環境變數。</span><span class="sxs-lookup"><span data-stu-id="c8190-170">All examples in hello following sections of this article assume that you've set hello `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="c8190-171">建立和管理 Blob</span><span class="sxs-lookup"><span data-stu-id="c8190-171">Create and manage blobs</span></span>
<span data-ttu-id="c8190-172">Azure Blob 儲存體是用於儲存大量非結構化資料，例如文字或二進位資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。</span><span class="sxs-lookup"><span data-stu-id="c8190-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="c8190-173">本節假設您已熟悉 Azure Blob 儲存體的概念。</span><span class="sxs-lookup"><span data-stu-id="c8190-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="c8190-174">如需詳細資訊，請參閱[使用 .NET 開始使用 Azure Blob 儲存體](../blobs/storage-dotnet-how-to-use-blobs.md)和 [Blob 服務概念](/rest/api/storageservices/blob-service-concepts)。</span><span class="sxs-lookup"><span data-stu-id="c8190-174">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="c8190-175">建立容器</span><span class="sxs-lookup"><span data-stu-id="c8190-175">Create a container</span></span>
<span data-ttu-id="c8190-176">Azure 儲存體中的每個 Blob 必須位於一個容器中。</span><span class="sxs-lookup"><span data-stu-id="c8190-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="c8190-177">您可以建立容器使用 hello`az storage container create`命令：</span><span class="sxs-lookup"><span data-stu-id="c8190-177">You can create a container by using hello `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="c8190-178">您可以為新的容器中設定的讀取權限的三個層級的其中一個，藉由指定選擇性的 hello`--public-access`引數：</span><span class="sxs-lookup"><span data-stu-id="c8190-178">You can set one of three levels of read access for a new container by specifying hello optional  `--public-access` argument:</span></span>

* <span data-ttu-id="c8190-179">`off`（預設值）： 容器資料為私用 toohello 帳戶擁有者。</span><span class="sxs-lookup"><span data-stu-id="c8190-179">`off` (default): Container data is private toohello account owner.</span></span>
* <span data-ttu-id="c8190-180">`blob`：Blob 的公用讀取權限。</span><span class="sxs-lookup"><span data-stu-id="c8190-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="c8190-181">`container`： 公用讀取和清單存取 toohello 整個容器。</span><span class="sxs-lookup"><span data-stu-id="c8190-181">`container`: Public read and list access toohello entire container.</span></span>

<span data-ttu-id="c8190-182">如需詳細資訊，請參閱[管理匿名讀取權限 toocontainers 和 blob](../blobs/storage-manage-access-to-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="c8190-182">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-tooa-container"></a><span data-ttu-id="c8190-183">上傳 blob tooa 容器</span><span class="sxs-lookup"><span data-stu-id="c8190-183">Upload a blob tooa container</span></span>
<span data-ttu-id="c8190-184">Azure Blob 儲存體支援區塊、附加和分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="c8190-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="c8190-185">上傳 blob tooa 容器使用 hello`blob upload`命令：</span><span class="sxs-lookup"><span data-stu-id="c8190-185">Upload blobs tooa container by using hello `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="c8190-186">根據預設，hello `blob upload` *.vhd 檔案 toopage blob 或區塊 blob 否則命令將上傳。</span><span class="sxs-lookup"><span data-stu-id="c8190-186">By default, hello `blob upload` command uploads *.vhd files toopage blobs, or block blobs otherwise.</span></span> <span data-ttu-id="c8190-187">另一個時輸入 toospecify 上傳 blob，您可以使用 hello`--type`引數--允許的值是`append`， `block`，和`page`。</span><span class="sxs-lookup"><span data-stu-id="c8190-187">toospecify another type when you upload a blob, you can use hello `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="c8190-188">如需有關 hello 不同的 blob 類型的詳細資訊，請參閱[了解區塊 Blob、 附加 Blob 和分頁 Blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs)。</span><span class="sxs-lookup"><span data-stu-id="c8190-188">For more information on hello different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="c8190-189">從容器下載 Blob</span><span class="sxs-lookup"><span data-stu-id="c8190-189">Download a blob from a container</span></span>
<span data-ttu-id="c8190-190">這個範例會示範如何 toodownload 從容器的 blob:</span><span class="sxs-lookup"><span data-stu-id="c8190-190">This example demonstrates how toodownload a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="c8190-191">列出容器中的 hello blob</span><span class="sxs-lookup"><span data-stu-id="c8190-191">List hello blobs in a container</span></span>

<span data-ttu-id="c8190-192">列出在 hello 與容器中的 hello blob [az 儲存體 blob 清單](/cli/azure/storage/blob#list)命令。</span><span class="sxs-lookup"><span data-stu-id="c8190-192">List hello blobs in a container with hello [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="c8190-193">複製 Blob</span><span class="sxs-lookup"><span data-stu-id="c8190-193">Copy blobs</span></span>
<span data-ttu-id="c8190-194">您可以在儲存體帳戶內或在不同儲存體帳戶和區域之間，以非同步方式複製 Blob。</span><span class="sxs-lookup"><span data-stu-id="c8190-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="c8190-195">hello 下列範例示範如何從一個儲存體 toocopy blob 帳戶 tooanother。</span><span class="sxs-lookup"><span data-stu-id="c8190-195">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="c8190-196">我們會先建立容器 hello 來源儲存體帳戶中，指定對其 blob 的公用讀取權。</span><span class="sxs-lookup"><span data-stu-id="c8190-196">We first create a container in hello source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="c8190-197">接下來，我們會將檔案 toohello 容器和最後，從該容器的複製 hello blob 上載到 hello 目的地儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="c8190-197">Next, we upload a file toohello container, and finally, copy hello blob from that container into a container in hello destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="c8190-198">在上述範例中的 hello，hello 目的地容器必須已存在於 hello 複製作業 toosucceed hello 目的地儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c8190-198">In hello above example, hello destination container must already exist in hello destination storage account for hello copy operation toosucceed.</span></span> <span data-ttu-id="c8190-199">此外，hello 來源 blob 中 hello 指定`--source-uri`引數必須包含共用的存取簽章 (SAS) 權杖，或為可公開存取，如此範例所示。</span><span class="sxs-lookup"><span data-stu-id="c8190-199">Additionally, hello source blob specified in hello `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="c8190-200">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="c8190-200">Delete a blob</span></span>
<span data-ttu-id="c8190-201">toodelete blob，使用 hello`blob delete`命令：</span><span class="sxs-lookup"><span data-stu-id="c8190-201">toodelete a blob, use hello `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="c8190-202">建立和管理檔案共用</span><span class="sxs-lookup"><span data-stu-id="c8190-202">Create and manage file shares</span></span>
<span data-ttu-id="c8190-203">Azure 檔案儲存體提供共用存放裝置使用 hello 伺服器訊息區塊 (SMB) 通訊協定的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c8190-203">Azure File storage offers shared storage for applications using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="c8190-204">Microsoft Azure 虛擬機器和雲端服務，以及內部部署應用程式，可以透過掛接共用，共用檔案資料。</span><span class="sxs-lookup"><span data-stu-id="c8190-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="c8190-205">您可以管理檔案共用和檔案資料，透過 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="c8190-205">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="c8190-206">如需 Azure 檔案儲存體的詳細資訊，請參閱[開始使用 Azure 檔案儲存在 Windows 上](../storage-dotnet-how-to-use-files.md)或[如何 toouse Linux 的 Azure 檔案儲存體](../storage-how-to-use-files-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="c8190-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="c8190-207">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="c8190-207">Create a file share</span></span>
<span data-ttu-id="c8190-208">Azure 檔案共用是 Azure 中的 SMB 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="c8190-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="c8190-209">所有目錄和檔案都必須在檔案共用中建立。</span><span class="sxs-lookup"><span data-stu-id="c8190-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="c8190-210">帳戶可以包含無限的數目的共用，並共用可以存放無限的數量的檔案，向上 toohello hello 儲存體帳戶的容量限制。</span><span class="sxs-lookup"><span data-stu-id="c8190-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="c8190-211">hello 下列範例會建立名為的檔案共用**myshare**。</span><span class="sxs-lookup"><span data-stu-id="c8190-211">hello following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="c8190-212">建立目錄</span><span class="sxs-lookup"><span data-stu-id="c8190-212">Create a directory</span></span>
<span data-ttu-id="c8190-213">目錄會提供 Azure 檔案共用的階層式結構。</span><span class="sxs-lookup"><span data-stu-id="c8190-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="c8190-214">hello 下列範例會建立一個名為目錄**myDir** hello 檔案共用中。</span><span class="sxs-lookup"><span data-stu-id="c8190-214">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="c8190-215">目錄路徑可包含多個層級，例如 **dir1/dir2**。</span><span class="sxs-lookup"><span data-stu-id="c8190-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="c8190-216">不過，您必須先確定所有父目錄都存在，才能建立子目錄。</span><span class="sxs-lookup"><span data-stu-id="c8190-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="c8190-217">例如，如果路徑是 **dir1/dir2**，您必須先建立目錄 **dir1**，然後再建立目錄 **dir2**。</span><span class="sxs-lookup"><span data-stu-id="c8190-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-tooa-share"></a><span data-ttu-id="c8190-218">上傳本機檔案 tooa 共用</span><span class="sxs-lookup"><span data-stu-id="c8190-218">Upload a local file tooa share</span></span>
<span data-ttu-id="c8190-219">hello 例會將檔案上傳從**~/temp/samplefile.txt**的 hello tooroot **myshare**檔案共用。</span><span class="sxs-lookup"><span data-stu-id="c8190-219">hello following example uploads a file from **~/temp/samplefile.txt** tooroot of hello **myshare** file share.</span></span> <span data-ttu-id="c8190-220">hello`--source`引數指定的現有本機檔案 tooupload hello。</span><span class="sxs-lookup"><span data-stu-id="c8190-220">hello `--source` argument specifies hello existing local file tooupload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="c8190-221">如同目錄建立時，您可以指定 hello 共用 tooupload hello 檔案 tooan 現有目錄內 hello 共用內的目錄路徑：</span><span class="sxs-lookup"><span data-stu-id="c8190-221">As with directory creation, you can specify a directory path within hello share tooupload hello file tooan existing directory within hello share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="c8190-222">Hello 共用中的檔案可以是 up too1 TB 的大小。</span><span class="sxs-lookup"><span data-stu-id="c8190-222">A file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-a-share"></a><span data-ttu-id="c8190-223">列出的共用中的 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="c8190-223">List hello files in a share</span></span>
<span data-ttu-id="c8190-224">您可以使用 hello 列出中共用檔案和目錄`az storage file list`命令：</span><span class="sxs-lookup"><span data-stu-id="c8190-224">You can list files and directories in a share by using hello `az storage file list` command:</span></span>

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="c8190-225">複製檔案</span><span class="sxs-lookup"><span data-stu-id="c8190-225">Copy files</span></span>      
<span data-ttu-id="c8190-226">您可以複製檔案 tooanother 檔案、 檔案 tooa blob 或 blob tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="c8190-226">You can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="c8190-227">例如，toocopy 中不同的共用檔案 tooa 目錄：</span><span class="sxs-lookup"><span data-stu-id="c8190-227">For example, toocopy a file tooa directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="c8190-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8190-228">Next steps</span></span>
<span data-ttu-id="c8190-229">以下是進一步了解使用 Azure CLI 2.0 hello 一些額外的資源。</span><span class="sxs-lookup"><span data-stu-id="c8190-229">Here are some additional resources for learning more about working with hello Azure CLI 2.0.</span></span>

* [<span data-ttu-id="c8190-230">開始使用 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c8190-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="c8190-231">Azure CLI 2.0 命令參考</span><span class="sxs-lookup"><span data-stu-id="c8190-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="c8190-232">GitHub 上的 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c8190-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
