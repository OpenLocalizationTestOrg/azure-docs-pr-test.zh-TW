---
title: "使用 Azure CLI 1.0 搭配 Azure 儲存體 | Microsoft Docs"
description: "了解如何使用「Azure 命令列介面」(Azure CLI) 1.0 搭配「Azure 儲存體」來建立和管理儲存體帳戶，以及處理 Azure Blob 和檔案。 Azure CLI 是一種跨平台工具"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: b246d8813a41d353a9c0fa31fe838e025fc93046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-10-with-azure-storage"></a><span data-ttu-id="fd21a-104">使用 Azure CLI 1.0 搭配 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="fd21a-104">Using the Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="fd21a-105">概觀</span><span class="sxs-lookup"><span data-stu-id="fd21a-105">Overview</span></span>

<span data-ttu-id="fd21a-106">Azure CLI 提供您一組開放原始碼的跨平台命令集合，供您運用在 Azure 平台上。</span><span class="sxs-lookup"><span data-stu-id="fd21a-106">The Azure CLI provides a set of open source, cross-platform commands for working with the Azure Platform.</span></span> <span data-ttu-id="fd21a-107">它提供許多與 [Azure 入口網站](https://portal.azure.com) 相同的功能，以及豐富的資料存取功能。</span><span class="sxs-lookup"><span data-stu-id="fd21a-107">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="fd21a-108">在本指南中，我們將探討如何使用 [Azure 命令列介面 (Azure CLI)](../cli-install-nodejs.md) 搭配「Azure 儲存體」來執行各種開發和管理工作。</span><span class="sxs-lookup"><span data-stu-id="fd21a-108">In this guide, we'll explore how to use [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md) to perform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="fd21a-109">建議您在使用本指南之前，先下載並安裝或升級至最新的 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="fd21a-109">We recommend that you download and install or upgrade to the latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="fd21a-110">本指南假設您已了解 Azure 儲存體的基本概念。</span><span class="sxs-lookup"><span data-stu-id="fd21a-110">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="fd21a-111">本指南提供許多指令碼示範如何使用 Azure CLI 搭配 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="fd21a-111">The guide provides a number of scripts to demonstrate the usage of the Azure CLI with Azure Storage.</span></span> <span data-ttu-id="fd21a-112">在執行每個指令碼之前，請務必先根據您的組態更新指令碼變數。</span><span class="sxs-lookup"><span data-stu-id="fd21a-112">Be sure to update the script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="fd21a-113">本指南提供傳統儲存體帳戶的 Azure CLI 命令和指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="fd21a-113">The guide provides the Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="fd21a-114">如需 Resource Manager 儲存體帳戶適用的 Azure CLI 命令，請參閱 [使用適用於 Mac、Linux 和 Windows 的 Azure CLI 搭配 Azure 資源管理](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) 。</span><span class="sxs-lookup"><span data-stu-id="fd21a-114">See [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-the-azure-cli-in-5-minutes"></a><span data-ttu-id="fd21a-115">在 5 分鐘內開始使用 Azure 儲存體和 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fd21a-115">Get started with Azure Storage and the Azure CLI in 5 minutes</span></span>
<span data-ttu-id="fd21a-116">本指南使用 Ubuntu 作為範例，但其他作業系統平台也同樣能夠執行。</span><span class="sxs-lookup"><span data-stu-id="fd21a-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="fd21a-117">**Azure 新手：** 取得 Microsoft Azure 訂用帳戶和與該訂用帳戶相關聯的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd21a-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="fd21a-118">如需 Azure 購買選項的資訊，請參閱[免費試用](https://azure.microsoft.com/pricing/free-trial/)、[購買選項](https://azure.microsoft.com/pricing/purchase-options/)和[會員優惠](https://azure.microsoft.com/pricing/member-offers/) (適用於 MSDN、Microsoft 合作夥伴網路、BizSpark 和其他 Microsoft 方案的成員)。</span><span class="sxs-lookup"><span data-stu-id="fd21a-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="fd21a-119">如需 Azure 訂用帳戶的詳細資訊，請參閱 [在 Azure Active Directory (Azure AD) 中指派系統管理員角色](https://msdn.microsoft.com/library/azure/hh531793.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="fd21a-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="fd21a-120">**建立 Microsoft Azure 訂用帳戶和帳戶之後：**</span><span class="sxs-lookup"><span data-stu-id="fd21a-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="fd21a-121">依照 [安裝 Azure CLI](../cli-install-nodejs.md)中的指示下載並安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="fd21a-121">Download and install the Azure CLI following the instructions outlined in [Install the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="fd21a-122">安裝好 Azure CLI 之後，您就能從命令列介面 (Bash、終端機、命令提示字元) 中使用 azure 命令存取 Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="fd21a-122">Once the Azure CLI has been installed, you will be able to use the azure command from your command-line interface (Bash, Terminal, Command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="fd21a-123">輸入 _azure_ 命令，您應該會看見下列輸出。</span><span class="sxs-lookup"><span data-stu-id="fd21a-123">Type the _azure_ command and you should see the following output.</span></span>

    ![Azure 命令輸出][Image1]
3. <span data-ttu-id="fd21a-125">在命令列介面中，輸入 `azure storage` 以列出所有 Azure 儲存體命令，對 Azure CLI 所提供的功能進行初步了解。</span><span class="sxs-lookup"><span data-stu-id="fd21a-125">In the command-line interface, type `azure storage` to list out all the azure storage commands and get a first impression of the functionalities the Azure CLI provides.</span></span> <span data-ttu-id="fd21a-126">您可以輸入命令名稱搭配 **-h** 參數 (例如，`azure storage share create -h`)，查看命令語法的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fd21a-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) to see details of command syntax.</span></span>
4. <span data-ttu-id="fd21a-127">現在，我們將提供您一個簡單的指令碼，其中顯示用來存取「Azure 儲存體」的基本 Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="fd21a-127">Now, we'll give you a simple script that shows basic Azure CLI commands to access Azure Storage.</span></span> <span data-ttu-id="fd21a-128">指令碼會先要求您為您的儲存體帳戶和金鑰設定兩個變數。</span><span class="sxs-lookup"><span data-stu-id="fd21a-128">The script will first ask you to set two variables for your storage account and key.</span></span> <span data-ttu-id="fd21a-129">然後，指令碼將在這個新的儲存體帳戶中建立新容器，並將現有的映像檔案 (Blob) 上傳至該容器。</span><span class="sxs-lookup"><span data-stu-id="fd21a-129">Then, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="fd21a-130">指令碼列出該容器中的所有 Blob 之後，會將映像檔案下載至本機電腦上的目的地目錄。</span><span class="sxs-lookup"><span data-stu-id="fd21a-130">After the script lists all blobs in that container, it will download the image file to the destination directory which exists on the local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating the container..."
    azure storage container create $container_name

    echo "Uploading the image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing the blobs..."
    azure storage blob list $container_name

    echo "Downloading the image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="fd21a-131">在您的本機電腦上，開啟您慣用的文字編輯器 (例如 vim)。</span><span class="sxs-lookup"><span data-stu-id="fd21a-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="fd21a-132">在文字編輯器中輸入上述指令碼。</span><span class="sxs-lookup"><span data-stu-id="fd21a-132">Type the above script into your text editor.</span></span>
6. <span data-ttu-id="fd21a-133">現在，您需要根據您的組態設定更新指令碼變數。</span><span class="sxs-lookup"><span data-stu-id="fd21a-133">Now, you need to update the script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="fd21a-134">**<storage_account_name>** 使用指令碼中的指定名稱，或是為儲存體帳戶輸入新名稱。</span><span class="sxs-lookup"><span data-stu-id="fd21a-134">**<storage_account_name>** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="fd21a-135">**重要事項：** 儲存體帳戶的名稱在 Azure 中必須是唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="fd21a-135">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="fd21a-136">而且必須是小寫字母！</span><span class="sxs-lookup"><span data-stu-id="fd21a-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="fd21a-137">**<storage_account_key>** 儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="fd21a-137">**<storage_account_key>** The access key of your storage account.</span></span>
   * <span data-ttu-id="fd21a-138">**<container_name>** 使用指令碼中的指定名稱，或是為容器輸入新名稱。</span><span class="sxs-lookup"><span data-stu-id="fd21a-138">**<container_name>** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="fd21a-139">**<image_to_upload>** 輸入位於本機電腦上的圖片路徑，例如 "~/images/HelloWorld.png"。</span><span class="sxs-lookup"><span data-stu-id="fd21a-139">**<image_to_upload>** Enter a path to a picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="fd21a-140">**<destination_folder>** 輸入用以儲存從「Azure 儲存體」下載之檔案的本機目錄路徑，例如 "~/downloadImages"。</span><span class="sxs-lookup"><span data-stu-id="fd21a-140">**<destination_folder>** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="fd21a-141">在 vim 中更新必要變數之後，請按下按鍵組合 `ESC`、`:`、`wq!` 來儲存指令碼。</span><span class="sxs-lookup"><span data-stu-id="fd21a-141">After you've updated the necessary variables in vim, press key combinations `ESC`, `:`, `wq!` to save the script.</span></span>
8. <span data-ttu-id="fd21a-142">若要執行這個指令碼，只要在 bash 主控台中輸入指令碼檔案名稱即可。</span><span class="sxs-lookup"><span data-stu-id="fd21a-142">To run this script, simply type the script file name in the bash console.</span></span> <span data-ttu-id="fd21a-143">在這個指令碼執行之後，您應該會有一個本機目的地資料夾，包含下載的映像檔案。</span><span class="sxs-lookup"><span data-stu-id="fd21a-143">After this script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="fd21a-144">以下螢幕擷取畫面顯示範例輸出︰</span><span class="sxs-lookup"><span data-stu-id="fd21a-144">The following screenshot shows an example output:</span></span>

<span data-ttu-id="fd21a-145">在指令碼執行之後，您應該有包含下載的映像檔案的本機目的資料夾。</span><span class="sxs-lookup"><span data-stu-id="fd21a-145">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-the-azure-cli"></a><span data-ttu-id="fd21a-146">使用 Azure CLI 管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="fd21a-146">Manage storage accounts with the Azure CLI</span></span>
### <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="fd21a-147">連接到 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fd21a-147">Connect to your Azure subscription</span></span>
<span data-ttu-id="fd21a-148">雖然大多數儲存體命令在沒有 Azure 訂用帳戶的情況下也能運作，但是仍建議您從 Azure CLI 連接到您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd21a-148">While most of the storage commands will work without an Azure subscription, we recommend you to connect to your subscription from the Azure CLI.</span></span> <span data-ttu-id="fd21a-149">若要設定讓 Azure CLI 與您的訂用帳戶搭配運作，請依照 [從 Azure CLI 連接到 Azure 訂用帳戶](../xplat-cli-connect.md)中的步驟操作。</span><span class="sxs-lookup"><span data-stu-id="fd21a-149">To configure the Azure CLI to work with your subscription, follow the steps in [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="fd21a-150">建立新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="fd21a-150">Create a new storage account</span></span>
<span data-ttu-id="fd21a-151">若要使用 Azure 儲存體，您將需要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd21a-151">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="fd21a-152">設定電腦以連接至您的訂用帳戶之後，您可以建立新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd21a-152">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="fd21a-153">儲存體帳戶的名稱必須介於 3 到 24 個字元的長度，而且只能使用數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="fd21a-153">The name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="fd21a-154">在環境變數中設定預設 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="fd21a-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="fd21a-155">您可以在訂用帳戶中有多個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd21a-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="fd21a-156">您可以選擇其中一個儲存體帳戶並且在環境變數中進行設定，讓同一個工作階段中的所有儲存體命令都能使用。</span><span class="sxs-lookup"><span data-stu-id="fd21a-156">You can choose one of them and set it in the environment variables for all the storage commands in the same session.</span></span> <span data-ttu-id="fd21a-157">這可讓您執行 Azure CLI 儲存體命令，而不需明確指定儲存體帳戶和金鑰。</span><span class="sxs-lookup"><span data-stu-id="fd21a-157">This enables you to run the Azure CLI storage commands without specifying the storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="fd21a-158">另一種設定預設儲存體帳戶的方式是使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="fd21a-158">Another way to set a default storage account is using connection string.</span></span> <span data-ttu-id="fd21a-159">首先透過下列命令取得連接字串：</span><span class="sxs-lookup"><span data-stu-id="fd21a-159">Firstly get the connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="fd21a-160">然後複製輸出連接字串，並將它設定為環境變數：</span><span class="sxs-lookup"><span data-stu-id="fd21a-160">Then copy the output connection string and set it to environment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="fd21a-161">建立和管理 Blob</span><span class="sxs-lookup"><span data-stu-id="fd21a-161">Create and manage blobs</span></span>
<span data-ttu-id="fd21a-162">Azure Blob 儲存體是一項儲存大量非結構化資料的服務 (例如文字或二進位資料)，全球任何地方都可透過 HTTP 或 HTTPS 來存取這些資料。</span><span class="sxs-lookup"><span data-stu-id="fd21a-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="fd21a-163">本節假設您已熟悉 Azure Blob 儲存體的概念。</span><span class="sxs-lookup"><span data-stu-id="fd21a-163">This section assumes that you are already familiar with the Azure Blob storage concepts.</span></span> <span data-ttu-id="fd21a-164">如需詳細資訊，請參閱[使用 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md)和 [Blob 服務概念](http://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fd21a-164">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="fd21a-165">建立容器</span><span class="sxs-lookup"><span data-stu-id="fd21a-165">Create a container</span></span>
<span data-ttu-id="fd21a-166">Azure 儲存體中的每個 Blob 必須位於一個容器中。</span><span class="sxs-lookup"><span data-stu-id="fd21a-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="fd21a-167">您可以使用 `azure storage container create` 命令建立私用容器：</span><span class="sxs-lookup"><span data-stu-id="fd21a-167">You can create a private container using the `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="fd21a-168">匿名讀取權限有三個層級：**Off**、**Blob** 和 **Container**。</span><span class="sxs-lookup"><span data-stu-id="fd21a-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="fd21a-169">若要防止匿名存取 Blob，請將 Permission 參數設定為 **Off**。</span><span class="sxs-lookup"><span data-stu-id="fd21a-169">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="fd21a-170">新容器預設為私人，且只能由帳戶擁有者存取。</span><span class="sxs-lookup"><span data-stu-id="fd21a-170">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="fd21a-171">若要允許 Blob 資源的匿名公開讀取權限，但不允許容器中繼資料或容器中 Blob 清單的匿名公開讀取權限，請將 Permission 參數設定為 **Blob**。</span><span class="sxs-lookup"><span data-stu-id="fd21a-171">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="fd21a-172">若要允許 Blob 資源、容器中繼資料或容器中 Blob 清單的完整公開讀取權限，請將 Permission 參數設定為 **Container**。</span><span class="sxs-lookup"><span data-stu-id="fd21a-172">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="fd21a-173">如需詳細資訊，請參閱 [管理對容器與 Blob 的匿名讀取權限](storage-manage-access-to-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="fd21a-173">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="fd21a-174">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="fd21a-174">Upload a blob into a container</span></span>
<span data-ttu-id="fd21a-175">Azure Blob 儲存體支援區塊 Blob 和頁面 Blob。</span><span class="sxs-lookup"><span data-stu-id="fd21a-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="fd21a-176">如需詳細資訊，請參閱 [了解區塊 Blob、附加 Blob 和分頁 Blob](http://msdn.microsoft.com/library/azure/ee691964.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fd21a-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="fd21a-177">若要將 Blob 上傳至容器，您可以使用 `azure storage blob upload`。</span><span class="sxs-lookup"><span data-stu-id="fd21a-177">To upload blobs in to a container, you can use the `azure storage blob upload`.</span></span> <span data-ttu-id="fd21a-178">根據預設，此命令會將本機檔案上傳至區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="fd21a-178">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="fd21a-179">若要指定 Blob 的類型，您可以使用 `--blobtype` 參數。</span><span class="sxs-lookup"><span data-stu-id="fd21a-179">To specify the type for the blob, you can use the `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="fd21a-180">從容器下載 Blob</span><span class="sxs-lookup"><span data-stu-id="fd21a-180">Download blobs from a container</span></span>
<span data-ttu-id="fd21a-181">下列範例示範如何從容器下載 Blob。</span><span class="sxs-lookup"><span data-stu-id="fd21a-181">The following example demonstrates how to download blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="fd21a-182">複製 Blob</span><span class="sxs-lookup"><span data-stu-id="fd21a-182">Copy blobs</span></span>
<span data-ttu-id="fd21a-183">您可以在儲存體帳戶內或在不同儲存體帳戶和區域之間，以非同步方式複製 Blob。</span><span class="sxs-lookup"><span data-stu-id="fd21a-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="fd21a-184">下列範例示範如何從一個儲存體帳戶複製 Blob 到另一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd21a-184">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="fd21a-185">在此範例中，我們建立 Blob 為公開，可匿名存取的容器。</span><span class="sxs-lookup"><span data-stu-id="fd21a-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="fd21a-186">此範例會執行非同步複製。</span><span class="sxs-lookup"><span data-stu-id="fd21a-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="fd21a-187">您可以執行 `azure storage blob copy show` 作業監視每個複製作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="fd21a-187">You can monitor the status of each copy operation by running the `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="fd21a-188">請注意，針對複製作業提供的來源 URL 必須是可公開存取，或包含 SAS (共用存取簽章) 權杖。</span><span class="sxs-lookup"><span data-stu-id="fd21a-188">Note that the source URL provided for the copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="fd21a-189">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="fd21a-189">Delete a blob</span></span>
<span data-ttu-id="fd21a-190">若要刪除 Blob，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="fd21a-190">To delete a blob, use the below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="fd21a-191">建立和管理檔案共用</span><span class="sxs-lookup"><span data-stu-id="fd21a-191">Create and manage file shares</span></span>
<span data-ttu-id="fd21a-192">Azure 檔案儲存體為使用標準 SMB 通訊協定的應用程式提供共用儲存體。</span><span class="sxs-lookup"><span data-stu-id="fd21a-192">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="fd21a-193">Microsoft Azure 虛擬機器和雲端服務，以及內部部署應用程式，可以透過掛接共用，共用檔案資料。</span><span class="sxs-lookup"><span data-stu-id="fd21a-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="fd21a-194">您可以透過 Azure CLI 管理檔案共用和檔案資料。</span><span class="sxs-lookup"><span data-stu-id="fd21a-194">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="fd21a-195">如需 Azure 檔案儲存體的詳細資訊，請參閱[在 Windows 上開始使用 Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)或[如何搭配 Linux 使用 Azure 檔案儲存體](storage-how-to-use-files-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="fd21a-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="fd21a-196">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="fd21a-196">Create a file share</span></span>
<span data-ttu-id="fd21a-197">Azure 檔案共用是 Azure 中的 SMB 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="fd21a-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="fd21a-198">所有目錄和檔案都必須在檔案共用中建立。</span><span class="sxs-lookup"><span data-stu-id="fd21a-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="fd21a-199">帳戶可包含無限制數目的共用，而共用可儲存無限制數目的檔案，最多可達儲存體帳戶的容量限制。</span><span class="sxs-lookup"><span data-stu-id="fd21a-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="fd21a-200">下列範例會建立名為 **myshare** 的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="fd21a-200">The following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="fd21a-201">建立目錄</span><span class="sxs-lookup"><span data-stu-id="fd21a-201">Create a directory</span></span>
<span data-ttu-id="fd21a-202">目錄會提供 Azure 檔案共用選擇性的階層式結構。</span><span class="sxs-lookup"><span data-stu-id="fd21a-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="fd21a-203">下列範例會在檔案共用中建立名為 **myDir** 的目錄。</span><span class="sxs-lookup"><span data-stu-id="fd21a-203">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="fd21a-204">請注意，目錄路徑可包含多個層級，例如 **a/b**。</span><span class="sxs-lookup"><span data-stu-id="fd21a-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="fd21a-205">不過，您必須確定所有父目錄都存在。</span><span class="sxs-lookup"><span data-stu-id="fd21a-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="fd21a-206">例如，如果路徑是 **a/b**，您必須先建立目錄 **a**，然後再建立目錄 **b**。</span><span class="sxs-lookup"><span data-stu-id="fd21a-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-to-directory"></a><span data-ttu-id="fd21a-207">上傳本機檔案至目錄</span><span class="sxs-lookup"><span data-stu-id="fd21a-207">Upload a local file to directory</span></span>
<span data-ttu-id="fd21a-208">下列範例將從 **~/temp/samplefile.txt** 上傳檔案至 **myDir** 目錄。</span><span class="sxs-lookup"><span data-stu-id="fd21a-208">The following example uploads a file from **~/temp/samplefile.txt** to the **myDir** directory.</span></span> <span data-ttu-id="fd21a-209">編輯檔案路徑，以指向本機機器上的有效檔案：</span><span class="sxs-lookup"><span data-stu-id="fd21a-209">Edit the file path so that it points to a valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="fd21a-210">請注意，共用中的檔案大小可能高達 1 TB。</span><span class="sxs-lookup"><span data-stu-id="fd21a-210">Note that a file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-the-share-root-or-directory"></a><span data-ttu-id="fd21a-211">列出共用根或目錄中的檔案</span><span class="sxs-lookup"><span data-stu-id="fd21a-211">List the files in the share root or directory</span></span>
<span data-ttu-id="fd21a-212">您可以使用下列命令，列出共用根或目錄中的檔案和子目錄：</span><span class="sxs-lookup"><span data-stu-id="fd21a-212">You can list the files and subdirectories in a share root or a directory using the following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="fd21a-213">請注意，列出作業不一定會顯示目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="fd21a-213">Note that the directory name is optional for the listing operation.</span></span> <span data-ttu-id="fd21a-214">如果省略，則命令會列出共用根目錄的內容。</span><span class="sxs-lookup"><span data-stu-id="fd21a-214">If omitted, the command lists the contents of the root directory of the share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="fd21a-215">複製檔案</span><span class="sxs-lookup"><span data-stu-id="fd21a-215">Copy files</span></span>
<span data-ttu-id="fd21a-216">從 Azure CLI 0.9.8 版開始，您可以將檔案複製到另一個檔案、將檔案複製到 Blob 或將 Blob 複製到檔案。</span><span class="sxs-lookup"><span data-stu-id="fd21a-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="fd21a-217">下列示範如何使用 CLI 命令執行這些複製作業。</span><span class="sxs-lookup"><span data-stu-id="fd21a-217">Below we demonstrate how to perform these copy operations using CLI commands.</span></span> <span data-ttu-id="fd21a-218">將檔案複製到新的目錄：</span><span class="sxs-lookup"><span data-stu-id="fd21a-218">To copy a file to the new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="fd21a-219">將 Blob 複製到檔案目錄：</span><span class="sxs-lookup"><span data-stu-id="fd21a-219">To copy a blob to a file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="fd21a-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd21a-220">Next Steps</span></span>

<span data-ttu-id="fd21a-221">您可以在下列網頁找到可與「儲存體」資源搭配運作的 Azure CLI 1.0 命令參考資料：</span><span class="sxs-lookup"><span data-stu-id="fd21a-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="fd21a-222">Resource Manager 模式中的 Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="fd21a-222">Azure CLI commands in Resource Manager mode</span></span>](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="fd21a-223">Azure 服務管理模式中的 Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="fd21a-223">Azure CLI commands in Azure Service Management mode</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="fd21a-224">您或許也會想要試試以 Python 撰寫的新一代 CLI [Azure CLI 2.0](storage-azure-cli.md)，此 CLI 可與 Resource Manager 部署模型搭配使用。</span><span class="sxs-lookup"><span data-stu-id="fd21a-224">You may also like to try the [Azure CLI 2.0](storage-azure-cli.md), our next-generation CLI written in Python, for use with the Resource Manager deployment model.</span></span>

[Image1]: ./media/storage-azure-cli/azure_command.png
