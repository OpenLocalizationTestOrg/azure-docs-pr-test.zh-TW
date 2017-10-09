---
title: "aaaHow toocreate Azure 檔案共用 |Microsoft 文件"
description: "如何 toocreate Azure 的檔案共用使用 hello Azure 入口網站、 PowerShell 和 hello Azure CLI Azure 檔案儲存體中。"
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 816694e411a993dae881816fc62173e2b7afe990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="61d72-103">在 Azure 檔案共用中建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="61d72-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="61d72-104">您可以建立使用 Azure 檔案共用[Azure 入口網站](https://portal.azure.com/)hello Azure 儲存體 PowerShell cmdlet、 hello Azure 儲存體用戶端程式庫，或 hello Azure 儲存體的 REST API。在本教學課程中，您將學習：</span><span class="sxs-lookup"><span data-stu-id="61d72-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="61d72-105">Toocreate Azure 檔案共用使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="61d72-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="61d72-106">如何 toocreate Azure 檔案共用使用 Powershell</span><span class="sxs-lookup"><span data-stu-id="61d72-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="61d72-107">如何 toocreate Azure 檔案共用使用 CLI</span><span class="sxs-lookup"><span data-stu-id="61d72-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="61d72-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="61d72-108">Prerequisites</span></span>
<span data-ttu-id="61d72-109">toocreate Azure 檔案共用，您可以使用的儲存體帳戶已經存在，或[建立新的 Azure 儲存體帳戶](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="61d72-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span> <span data-ttu-id="61d72-110">toocreate 使用 PowerShell 的 Azure 檔案共用，您將需要 hello 帳號金鑰及儲存體帳戶名稱...</span><span class="sxs-lookup"><span data-stu-id="61d72-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="61d72-111">如果您計劃 toouse Powershell 或 CLI，您需要儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="61d72-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="61d72-112">建立檔案共用，透過 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="61d72-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="61d72-113">**Azure 入口網站上的 [移 tooStorage 帳戶] 刀鋒視窗**:</span><span class="sxs-lookup"><span data-stu-id="61d72-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="61d72-114">![儲存體帳戶刀鋒視窗](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="61d72-114">![Storage Account Blade](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="61d72-115">**按一下 [新增檔案共用] 按鈕**：</span><span class="sxs-lookup"><span data-stu-id="61d72-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="61d72-116">![按一下 hello 新增檔案共用 按鈕](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="61d72-116">![Click hello add file share button](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="61d72-117">**提供名稱和配額。配額目前上限可以是 5TB**：</span><span class="sxs-lookup"><span data-stu-id="61d72-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="61d72-118">![提供的名稱和所需的配額的 hello 新檔案共用](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="61d72-118">![Provide a name and a desired quota for hello new file share](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="61d72-119">**檢視新的檔案共用**：![檢視新的檔案共用](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="61d72-119">**View your new file share**:  ![View your new file share](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="61d72-120">**上傳檔案**![上傳檔案](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="61d72-120">**Upload a file**:  ![Upload a file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="61d72-121">**瀏覽至檔案共用並管理您的目錄和檔案**：![瀏覽檔案共用](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="61d72-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="61d72-122">透過 PowerShell 建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="61d72-122">Create file share through PowerShell</span></span>
<span data-ttu-id="61d72-123">tooprepare toouse PowerShell 中，下載並安裝 hello Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="61d72-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="61d72-124">請參閱[如何 tooinstall 和設定 Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) hello 安裝點和安裝指示。</span><span class="sxs-lookup"><span data-stu-id="61d72-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="61d72-125">建議您下載並安裝或升級 toohello 最新的 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="61d72-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="61d72-126">**建立您的儲存體帳戶和金鑰內容**hello 內容封裝 hello 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="61d72-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="61d72-127">如需從 [Azure 入口網站](https://portal.azure.com/)複製帳戶金鑰的指示，請參閱[檢視和複製儲存體存取金鑰](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="61d72-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="61d72-128">**建立新的檔案共用**：</span><span class="sxs-lookup"><span data-stu-id="61d72-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="61d72-129">檔案共用的 hello 名稱必須全部小寫。</span><span class="sxs-lookup"><span data-stu-id="61d72-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="61d72-130">如需有關為檔案共用與檔案命名的完整詳細資料，請參閱 [命名和參考共用、目錄、檔案及中繼資料](https://msdn.microsoft.com/library/azure/dn167011.aspx)。</span><span class="sxs-lookup"><span data-stu-id="61d72-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="61d72-131">透過命令列介面 (CLI) 建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="61d72-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="61d72-132">**tooprepare toouse 命令列介面 (CLI)，下載並安裝 hello Azure CLI。**</span><span class="sxs-lookup"><span data-stu-id="61d72-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="61d72-133">請參閱[安裝 Azure CLI 2.0](/cli/azure/install-az-cli2.md) 和[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="61d72-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="61d72-134">**建立您想要 toocreate hello 共用的連線字串 toohello 儲存體帳戶。**</span><span class="sxs-lookup"><span data-stu-id="61d72-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="61d72-135">取代```<storage-account>```和```<resource_group>```與儲存體帳戶名稱和資源群組在下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="61d72-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="61d72-136">**建立檔案共用**</span><span class="sxs-lookup"><span data-stu-id="61d72-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="61d72-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61d72-137">Next steps</span></span>
* [<span data-ttu-id="61d72-138">連線並掛接檔案共用 - Windows</span><span class="sxs-lookup"><span data-stu-id="61d72-138">Connect and Mount File Share - Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="61d72-139">連線並掛接檔案共用 - Linux</span><span class="sxs-lookup"><span data-stu-id="61d72-139">Connect and Mount File Share - Linux</span></span>](../storage-how-to-use-files-linux.md)
* [<span data-ttu-id="61d72-140">連線並掛接檔案共用 - macOS</span><span class="sxs-lookup"><span data-stu-id="61d72-140">Connect and Mount File Share - macOS</span></span>](storage-how-to-use-files-mac.md)

<span data-ttu-id="61d72-141">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="61d72-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="61d72-142">常見問題集</span><span class="sxs-lookup"><span data-stu-id="61d72-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="61d72-143">在 Windows 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="61d72-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="61d72-144">在 Linux 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="61d72-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   