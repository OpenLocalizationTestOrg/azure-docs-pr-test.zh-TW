---
title: "aaaUsing hello Azure CLI 1.0 搭配 Azure 儲存體 |Microsoft 文件"
description: "了解 toouse hello Azure 命令列介面 (Azure CLI) 1.0 與 Azure 儲存體 toocreate 和管理儲存體帳戶和使用 Azure blob 及檔案的方式。 hello Azure CLI 是跨平台工具"
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
ms.openlocfilehash: 25e459403dde631741403c8722ed07beafac35c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a><span data-ttu-id="11532-104">使用 Azure CLI 1.0 hello 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="11532-104">Using hello Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="11532-105">概觀</span><span class="sxs-lookup"><span data-stu-id="11532-105">Overview</span></span>

<span data-ttu-id="11532-106">hello Azure CLI 提供一組的開放原始碼跨平台命令來處理 hello Azure 平台。</span><span class="sxs-lookup"><span data-stu-id="11532-106">hello Azure CLI provides a set of open source, cross-platform commands for working with hello Azure Platform.</span></span> <span data-ttu-id="11532-107">它可提供許多相同的功能位於 hello hello [Azure 入口網站](https://portal.azure.com)也為豐富的資料存取功能。</span><span class="sxs-lookup"><span data-stu-id="11532-107">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="11532-108">本指南中，我們將探討如何 toouse [Azure 命令列介面 (Azure CLI)](../../cli-install-nodejs.md) tooperform 各種開發和管理工作與 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="11532-108">In this guide, we'll explore how toouse [Azure Command-Line Interface (Azure CLI)](../../cli-install-nodejs.md) tooperform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="11532-109">我們建議您下載並安裝或升級 toohello 使用本指南之前的最新 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="11532-109">We recommend that you download and install or upgrade toohello latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="11532-110">本指南假設您已了解 hello 的 Azure 儲存體的基本概念。</span><span class="sxs-lookup"><span data-stu-id="11532-110">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="11532-111">hello 指南提供的指令碼數目的 hello 與 Azure 儲存體的 Azure CLI toodemonstrate hello 使用量。</span><span class="sxs-lookup"><span data-stu-id="11532-111">hello guide provides a number of scripts toodemonstrate hello usage of hello Azure CLI with Azure Storage.</span></span> <span data-ttu-id="11532-112">為確定 tooupdate hello 指令碼變數，根據您的設定，才能執行每個指令碼。</span><span class="sxs-lookup"><span data-stu-id="11532-112">Be sure tooupdate hello script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="11532-113">hello 指南提供傳統儲存體帳戶的 hello Azure CLI 命令和指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="11532-113">hello guide provides hello Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="11532-114">請參閱[使用 hello Mac、 Linux 和 Windows Azure 資源管理與 Azure CLI](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)資源管理員的儲存體帳戶的 Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="11532-114">See [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a><span data-ttu-id="11532-115">開始使用 Azure 儲存體和 hello Azure CLI 在 5 分鐘內</span><span class="sxs-lookup"><span data-stu-id="11532-115">Get started with Azure Storage and hello Azure CLI in 5 minutes</span></span>
<span data-ttu-id="11532-116">本指南使用 Ubuntu 作為範例，但其他作業系統平台也同樣能夠執行。</span><span class="sxs-lookup"><span data-stu-id="11532-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="11532-117">**新 tooAzure:**取得 Microsoft Azure 訂用帳戶和該訂用帳戶相關聯的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11532-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="11532-118">如需 Azure 購買選項的資訊，請參閱[免費試用](https://azure.microsoft.com/pricing/free-trial/)、[購買選項](https://azure.microsoft.com/pricing/purchase-options/)和[會員優惠](https://azure.microsoft.com/pricing/member-offers/) (適用於 MSDN、Microsoft 合作夥伴網路、BizSpark 和其他 Microsoft 方案的成員)。</span><span class="sxs-lookup"><span data-stu-id="11532-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="11532-119">如需 Azure 訂用帳戶的詳細資訊，請參閱 [在 Azure Active Directory (Azure AD) 中指派系統管理員角色](https://msdn.microsoft.com/library/azure/hh531793.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="11532-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="11532-120">**建立 Microsoft Azure 訂用帳戶和帳戶之後：**</span><span class="sxs-lookup"><span data-stu-id="11532-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="11532-121">下載並安裝 Azure CLI hello 指示中所述的 hello[安裝 hello Azure CLI](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="11532-121">Download and install hello Azure CLI following hello instructions outlined in [Install hello Azure CLI](../../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="11532-122">一旦 hello Azure CLI 安裝之後，您將無法 toouse hello azure 命令列介面 （Bash，終端機，命令提示字元） tooaccess hello Azure CLI 命令的命令。</span><span class="sxs-lookup"><span data-stu-id="11532-122">Once hello Azure CLI has been installed, you will be able toouse hello azure command from your command-line interface (Bash, Terminal, Command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="11532-123">型別 hello _azure_命令，而且您應該會看到下列輸出的 hello。</span><span class="sxs-lookup"><span data-stu-id="11532-123">Type hello _azure_ command and you should see hello following output.</span></span>

    ![Azure 命令輸出](./media/storage-azure-cli/azure_command.png)   
3. <span data-ttu-id="11532-125">在 hello 命令列介面中，輸入`azure storage`所有 toolist hello azure 儲存體命令，並取得 hello 功能 hello Azure CLI 提供第一印象。</span><span class="sxs-lookup"><span data-stu-id="11532-125">In hello command-line interface, type `azure storage` toolist out all hello azure storage commands and get a first impression of hello functionalities hello Azure CLI provides.</span></span> <span data-ttu-id="11532-126">您可以輸入命令名稱**-h**參數 (例如， `azure storage share create -h`) toosee 的命令語法的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="11532-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) toosee details of command syntax.</span></span>
4. <span data-ttu-id="11532-127">現在，我們會提供簡單的指令碼會顯示基本 Azure CLI 命令 tooaccess Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="11532-127">Now, we'll give you a simple script that shows basic Azure CLI commands tooaccess Azure Storage.</span></span> <span data-ttu-id="11532-128">hello 指令碼會先要求您 tooset 兩個變數提供您的儲存體帳戶和金鑰。</span><span class="sxs-lookup"><span data-stu-id="11532-128">hello script will first ask you tooset two variables for your storage account and key.</span></span> <span data-ttu-id="11532-129">然後，hello 指令碼會在這個新的儲存體帳戶中建立新的容器，並上傳現有的映像檔案 (blob) toothat 容器。</span><span class="sxs-lookup"><span data-stu-id="11532-129">Then, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="11532-130">Hello 指令碼會列出該容器中的所有 blob 之後，它會下載 hello 映像檔案 toohello 目的地目錄已存在 hello 本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="11532-130">After hello script lists all blobs in that container, it will download hello image file toohello destination directory which exists on hello local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="11532-131">在您的本機電腦上，開啟您慣用的文字編輯器 (例如 vim)。</span><span class="sxs-lookup"><span data-stu-id="11532-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="11532-132">在文字編輯器中輸入 hello 上述指令碼。</span><span class="sxs-lookup"><span data-stu-id="11532-132">Type hello above script into your text editor.</span></span>
6. <span data-ttu-id="11532-133">現在，您必須根據您的組態設定 tooupdate hello 指令碼變數。</span><span class="sxs-lookup"><span data-stu-id="11532-133">Now, you need tooupdate hello script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="11532-134">**< Storage_account_name >**使用給定名稱 hello 指令碼中的 hello 或輸入您的儲存體帳戶的新名稱。</span><span class="sxs-lookup"><span data-stu-id="11532-134">**<storage_account_name>** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="11532-135">**重要事項：** hello hello 儲存體帳戶名稱必須是唯一在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="11532-135">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="11532-136">而且必須是小寫字母！</span><span class="sxs-lookup"><span data-stu-id="11532-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="11532-137">**< storage_account_key >** hello 的儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="11532-137">**<storage_account_key>** hello access key of your storage account.</span></span>
   * <span data-ttu-id="11532-138">**< Container_name >**使用給定名稱 hello 指令碼中的 hello 或輸入您的容器的新名稱。</span><span class="sxs-lookup"><span data-stu-id="11532-138">**<container_name>** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="11532-139">**< Image_to_upload >**您本機電腦上，輸入路徑 tooa 圖片，例如:"~ / images/HelloWorld.png"。</span><span class="sxs-lookup"><span data-stu-id="11532-139">**<image_to_upload>** Enter a path tooa picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="11532-140">**< Destination_folder >** Enter 路徑 tooa 本機目錄 toostore 下載檔案，從 Azure 儲存體，例如:"~/downloadImages"。</span><span class="sxs-lookup"><span data-stu-id="11532-140">**<destination_folder>** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="11532-141">更新 vim 中的 hello 必要變數之後，按下按鍵組合`ESC`， `:`， `wq!` toosave hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="11532-141">After you've updated hello necessary variables in vim, press key combinations `ESC`, `:`, `wq!` toosave hello script.</span></span>
8. <span data-ttu-id="11532-142">toorun 此指令碼，只要類型 hello 指令碼檔案名稱 hello bash 主控台中。</span><span class="sxs-lookup"><span data-stu-id="11532-142">toorun this script, simply type hello script file name in hello bash console.</span></span> <span data-ttu-id="11532-143">執行這個指令碼之後，您應該有包含 hello 下載映像檔的本機目的資料夾。</span><span class="sxs-lookup"><span data-stu-id="11532-143">After this script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="11532-144">下列螢幕擷取畫面的 hello 顯示範例輸出：</span><span class="sxs-lookup"><span data-stu-id="11532-144">hello following screenshot shows an example output:</span></span>

<span data-ttu-id="11532-145">Hello 指令碼執行之後，您應該有包含 hello 下載映像檔的本機目的資料夾。</span><span class="sxs-lookup"><span data-stu-id="11532-145">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-hello-azure-cli"></a><span data-ttu-id="11532-146">管理儲存體帳戶以 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="11532-146">Manage storage accounts with hello Azure CLI</span></span>
### <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="11532-147">連接 tooyour Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="11532-147">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="11532-148">雖然大部分 hello 儲存命令的運作時不會具有 Azure 訂用帳戶，但建議您從 hello Azure CLI tooconnect tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="11532-148">While most of hello storage commands will work without an Azure subscription, we recommend you tooconnect tooyour subscription from hello Azure CLI.</span></span> <span data-ttu-id="11532-149">tooconfigure hello Azure CLI toowork 與您的訂用帳戶，請依照下列中的 hello 步驟[tooan Azure 訂用帳戶連線從 hello Azure CLI](../../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="11532-149">tooconfigure hello Azure CLI toowork with your subscription, follow hello steps in [Connect tooan Azure subscription from hello Azure CLI](../../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="11532-150">建立新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="11532-150">Create a new storage account</span></span>
<span data-ttu-id="11532-151">toouse Azure 儲存體，您需要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="11532-151">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="11532-152">設定您的電腦 tooconnect tooyour 訂用帳戶之後，您可以建立新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="11532-152">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="11532-153">hello 您的儲存體帳戶名稱必須介於 3 到 24 個字元的長度，並使用數字和小寫的字母。</span><span class="sxs-lookup"><span data-stu-id="11532-153">hello name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="11532-154">在環境變數中設定預設 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="11532-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="11532-155">您可以在訂用帳戶中有多個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="11532-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="11532-156">您可以選擇其中一個，並將它設定在 hello 環境變數的所有 hello 存放裝置中的都命令 hello 相同工作階段。</span><span class="sxs-lookup"><span data-stu-id="11532-156">You can choose one of them and set it in hello environment variables for all hello storage commands in hello same session.</span></span> <span data-ttu-id="11532-157">這可讓您 toorun hello Azure CLI 儲存命令，而不指定 hello 儲存體帳戶，以及明確金鑰。</span><span class="sxs-lookup"><span data-stu-id="11532-157">This enables you toorun hello Azure CLI storage commands without specifying hello storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="11532-158">另一個方式 tooset 預設儲存體帳戶正在使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="11532-158">Another way tooset a default storage account is using connection string.</span></span> <span data-ttu-id="11532-159">首先命令以取得 hello 連接字串：</span><span class="sxs-lookup"><span data-stu-id="11532-159">Firstly get hello connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="11532-160">然後將複製 hello 輸出連接字串，並將它設定 tooenvironment 變數：</span><span class="sxs-lookup"><span data-stu-id="11532-160">Then copy hello output connection string and set it tooenvironment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="11532-161">建立和管理 Blob</span><span class="sxs-lookup"><span data-stu-id="11532-161">Create and manage blobs</span></span>
<span data-ttu-id="11532-162">Azure Blob 儲存體是用於儲存大量非結構化資料，例如文字或二進位資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。</span><span class="sxs-lookup"><span data-stu-id="11532-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="11532-163">本節假設您已熟悉 hello Azure Blob 儲存體概念。</span><span class="sxs-lookup"><span data-stu-id="11532-163">This section assumes that you are already familiar with hello Azure Blob storage concepts.</span></span> <span data-ttu-id="11532-164">如需詳細資訊，請參閱[使用 .NET 開始使用 Azure Blob 儲存體](../blobs/storage-dotnet-how-to-use-blobs.md)和 [Blob 服務概念](http://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="11532-164">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="11532-165">建立容器</span><span class="sxs-lookup"><span data-stu-id="11532-165">Create a container</span></span>
<span data-ttu-id="11532-166">Azure 儲存體中的每個 Blob 必須位於一個容器中。</span><span class="sxs-lookup"><span data-stu-id="11532-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="11532-167">您可以建立私用容器使用 hello`azure storage container create`命令：</span><span class="sxs-lookup"><span data-stu-id="11532-167">You can create a private container using hello `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="11532-168">匿名讀取權限有三個層級：**Off**、**Blob** 和 **Container**。</span><span class="sxs-lookup"><span data-stu-id="11532-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="11532-169">tooprevent 匿名存取 tooblobs，集 hello 權限的參數太**關閉**。</span><span class="sxs-lookup"><span data-stu-id="11532-169">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="11532-170">根據預設，hello 新容器是私人的而且只有 hello 帳戶擁有者可存取。</span><span class="sxs-lookup"><span data-stu-id="11532-170">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="11532-171">tooallow 匿名公用讀取存取 tooblob 資源，但不是 toocontainer 中繼資料或 toohello 清單 hello 容器中的 blob、 設定 hello 權限的參數太**Blob**。</span><span class="sxs-lookup"><span data-stu-id="11532-171">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="11532-172">tooallow 完整公用讀取存取 tooblob 資源、 容器中繼資料及 hello hello 容器中的 blob 清單中，設定 hello 權限的參數太**容器**。</span><span class="sxs-lookup"><span data-stu-id="11532-172">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="11532-173">如需詳細資訊，請參閱[管理匿名讀取權限 toocontainers 和 blob](../blobs/storage-manage-access-to-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="11532-173">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="11532-174">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="11532-174">Upload a blob into a container</span></span>
<span data-ttu-id="11532-175">Azure Blob 儲存體支援區塊 Blob 和頁面 Blob。</span><span class="sxs-lookup"><span data-stu-id="11532-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="11532-176">如需詳細資訊，請參閱 [了解區塊 Blob、附加 Blob 和分頁 Blob](http://msdn.microsoft.com/library/azure/ee691964.aspx)。</span><span class="sxs-lookup"><span data-stu-id="11532-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="11532-177">tooupload tooa 容器中的 blob，您可以使用 hello `azure storage blob upload`。</span><span class="sxs-lookup"><span data-stu-id="11532-177">tooupload blobs in tooa container, you can use hello `azure storage blob upload`.</span></span> <span data-ttu-id="11532-178">根據預設，此命令會將 hello 本機檔案 tooa 區塊 blob 上傳。</span><span class="sxs-lookup"><span data-stu-id="11532-178">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="11532-179">toospecify hello hello blob 類型，您可以使用 hello`--blobtype`參數。</span><span class="sxs-lookup"><span data-stu-id="11532-179">toospecify hello type for hello blob, you can use hello `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="11532-180">從容器下載 Blob</span><span class="sxs-lookup"><span data-stu-id="11532-180">Download blobs from a container</span></span>
<span data-ttu-id="11532-181">下列範例中的 hello 示範 toodownload 從容器的 blob。</span><span class="sxs-lookup"><span data-stu-id="11532-181">hello following example demonstrates how toodownload blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="11532-182">複製 Blob</span><span class="sxs-lookup"><span data-stu-id="11532-182">Copy blobs</span></span>
<span data-ttu-id="11532-183">您可以在儲存體帳戶內或在不同儲存體帳戶和區域之間，以非同步方式複製 Blob。</span><span class="sxs-lookup"><span data-stu-id="11532-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="11532-184">hello 下列範例示範如何從一個儲存體 toocopy blob 帳戶 tooanother。</span><span class="sxs-lookup"><span data-stu-id="11532-184">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="11532-185">在此範例中，我們建立 Blob 為公開，可匿名存取的容器。</span><span class="sxs-lookup"><span data-stu-id="11532-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="11532-186">此範例會執行非同步複製。</span><span class="sxs-lookup"><span data-stu-id="11532-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="11532-187">您可以監視每個複製作業的 hello 狀態執行 hello`azure storage blob copy show`作業。</span><span class="sxs-lookup"><span data-stu-id="11532-187">You can monitor hello status of each copy operation by running hello `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="11532-188">請注意，hello 複製作業所提供的 hello 來源 URL 必須可公開存取，或包含 SAS （共用的存取簽章） 權杖。</span><span class="sxs-lookup"><span data-stu-id="11532-188">Note that hello source URL provided for hello copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="11532-189">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="11532-189">Delete a blob</span></span>
<span data-ttu-id="11532-190">toodelete blob，使用下列命令 hello:</span><span class="sxs-lookup"><span data-stu-id="11532-190">toodelete a blob, use hello below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="11532-191">建立和管理檔案共用</span><span class="sxs-lookup"><span data-stu-id="11532-191">Create and manage file shares</span></span>
<span data-ttu-id="11532-192">Azure 檔案儲存體提供共用存放裝置使用 hello 標準 SMB 通訊協定的應用程式。</span><span class="sxs-lookup"><span data-stu-id="11532-192">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="11532-193">Microsoft Azure 虛擬機器和雲端服務，以及內部部署應用程式，可以透過掛接共用，共用檔案資料。</span><span class="sxs-lookup"><span data-stu-id="11532-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="11532-194">您可以管理檔案共用和檔案資料，透過 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="11532-194">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="11532-195">如需 Azure 檔案儲存體的詳細資訊，請參閱[開始使用 Azure 檔案儲存在 Windows 上](../storage-dotnet-how-to-use-files.md)或[如何 toouse Linux 的 Azure 檔案儲存體](../storage-how-to-use-files-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="11532-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="11532-196">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="11532-196">Create a file share</span></span>
<span data-ttu-id="11532-197">Azure 檔案共用是 Azure 中的 SMB 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="11532-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="11532-198">所有目錄和檔案都必須在檔案共用中建立。</span><span class="sxs-lookup"><span data-stu-id="11532-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="11532-199">帳戶可以包含無限的數目的共用，並共用可以存放無限的數量的檔案，向上 toohello hello 儲存體帳戶的容量限制。</span><span class="sxs-lookup"><span data-stu-id="11532-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="11532-200">hello 下列範例會建立名為的檔案共用**myshare**。</span><span class="sxs-lookup"><span data-stu-id="11532-200">hello following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="11532-201">建立目錄</span><span class="sxs-lookup"><span data-stu-id="11532-201">Create a directory</span></span>
<span data-ttu-id="11532-202">目錄會提供 Azure 檔案共用選擇性的階層式結構。</span><span class="sxs-lookup"><span data-stu-id="11532-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="11532-203">hello 下列範例會建立一個名為目錄**myDir** hello 檔案共用中。</span><span class="sxs-lookup"><span data-stu-id="11532-203">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="11532-204">請注意，目錄路徑可包含多個層級，例如 **a/b**。</span><span class="sxs-lookup"><span data-stu-id="11532-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="11532-205">不過，您必須確定所有父目錄都存在。</span><span class="sxs-lookup"><span data-stu-id="11532-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="11532-206">例如，如果路徑是 **a/b**，您必須先建立目錄 **a**，然後再建立目錄 **b**。</span><span class="sxs-lookup"><span data-stu-id="11532-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-toodirectory"></a><span data-ttu-id="11532-207">上傳本機檔案 toodirectory</span><span class="sxs-lookup"><span data-stu-id="11532-207">Upload a local file toodirectory</span></span>
<span data-ttu-id="11532-208">hello 例會將檔案上傳從**~/temp/samplefile.txt** toohello **myDir**目錄。</span><span class="sxs-lookup"><span data-stu-id="11532-208">hello following example uploads a file from **~/temp/samplefile.txt** toohello **myDir** directory.</span></span> <span data-ttu-id="11532-209">編輯 hello 檔案路徑，使它所指 tooa 有效的檔案在本機電腦上：</span><span class="sxs-lookup"><span data-stu-id="11532-209">Edit hello file path so that it points tooa valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="11532-210">請注意，在 hello 共用的檔案可以是 up too1 TB 的大小。</span><span class="sxs-lookup"><span data-stu-id="11532-210">Note that a file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-hello-share-root-or-directory"></a><span data-ttu-id="11532-211">列出 hello 共用根目錄或目錄中的 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="11532-211">List hello files in hello share root or directory</span></span>
<span data-ttu-id="11532-212">您可以列出 hello 檔案和子目錄的共用根目錄或使用下列命令的 hello 目錄中：</span><span class="sxs-lookup"><span data-stu-id="11532-212">You can list hello files and subdirectories in a share root or a directory using hello following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="11532-213">請注意該 hello 目錄名稱是選擇性的 hello 列出作業。</span><span class="sxs-lookup"><span data-stu-id="11532-213">Note that hello directory name is optional for hello listing operation.</span></span> <span data-ttu-id="11532-214">如果省略，則 hello 命令會列出 hello hello 根目錄 hello 共用的內容。</span><span class="sxs-lookup"><span data-stu-id="11532-214">If omitted, hello command lists hello contents of hello root directory of hello share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="11532-215">複製檔案</span><span class="sxs-lookup"><span data-stu-id="11532-215">Copy files</span></span>
<span data-ttu-id="11532-216">開始使用 Azure CLI 0.9.8 版，您可以複製檔案 tooanother 檔案、 檔案 tooa blob 或 blob tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="11532-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="11532-217">下面我們將示範如何 tooperform 這些複製使用 CLI 命令的作業。</span><span class="sxs-lookup"><span data-stu-id="11532-217">Below we demonstrate how tooperform these copy operations using CLI commands.</span></span> <span data-ttu-id="11532-218">toocopy toohello 新檔案的目錄：</span><span class="sxs-lookup"><span data-stu-id="11532-218">toocopy a file toohello new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="11532-219">toocopy blob tooa 檔案目錄：</span><span class="sxs-lookup"><span data-stu-id="11532-219">toocopy a blob tooa file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="11532-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11532-220">Next Steps</span></span>

<span data-ttu-id="11532-221">您可以在下列網頁找到可與「儲存體」資源搭配運作的 Azure CLI 1.0 命令參考資料：</span><span class="sxs-lookup"><span data-stu-id="11532-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="11532-222">Resource Manager 模式中的 Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="11532-222">Azure CLI commands in Resource Manager mode</span></span>](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="11532-223">Azure 服務管理模式中的 Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="11532-223">Azure CLI commands in Azure Service Management mode</span></span>](../../cli-install-nodejs.md)

<span data-ttu-id="11532-224">您可能也要 tootry hello [Azure CLI 2.0](../storage-azure-cli.md)、 撰寫搭配 hello Resource Manager 部署模型使用 Python，我們下一代 CLI。</span><span class="sxs-lookup"><span data-stu-id="11532-224">You may also like tootry hello [Azure CLI 2.0](../storage-azure-cli.md), our next-generation CLI written in Python, for use with hello Resource Manager deployment model.</span></span>
